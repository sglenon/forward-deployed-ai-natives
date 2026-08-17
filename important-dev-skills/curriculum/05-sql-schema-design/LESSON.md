# Lesson: make data relationships executable

## Learning goals

You will design a small relational schema, name invariants, enforce them with SQLite constraints, query relationships with parameters, and reason about migrations and deletion.

## Relational vocabulary

A **database** stores data. A **table** groups records with the same columns. A **row** is one record; a **column** is one named attribute. A **primary key** uniquely identifies a row. A **foreign key** stores a reference to a primary key in another table. **Cardinality** describes how many related records are allowed: one-to-many or many-to-many.

Our scenario has `learners`, `courses`, `sections`, and `enrollments`. A learner can enroll in many courses and a course can contain many learners: that is many-to-many, represented by a relationship table (`enrollments`) with one row per pair. Repeating `course_1`, `course_2` columns would create a fixed, awkward limit.

## Invariants before SQL

An **invariant** is a fact that must always be true. Write them first: learner names are required; course codes are unique; an enrollment references existing learner/course rows; one learner cannot enroll in the same course twice; status is one of `active`, `completed`, `cancelled`. Constraints are executable documentation:

```sql
CREATE TABLE enrollments (
  learner_id INTEGER NOT NULL REFERENCES learners(id) ON DELETE CASCADE,
  course_id INTEGER NOT NULL REFERENCES courses(id) ON DELETE RESTRICT,
  status TEXT NOT NULL CHECK (status IN ('active','completed','cancelled')),
  PRIMARY KEY (learner_id, course_id)
)
```

`NOT NULL` prevents omission, `UNIQUE` prevents duplicates, `CHECK` limits values, and `FOREIGN KEY` prevents orphans. SQLite foreign-key enforcement must be enabled with `PRAGMA foreign_keys = ON`; the notebook does this explicitly.

## Normalization and source of truth

**Normalization** means storing each changing fact in one appropriate place and relating it by keys. It reduces contradictory copies. A denormalized column is a deliberate duplicate for a measured read need. If you store `course.enrollment_count`, document that `enrollments` is the source of truth, who updates the count, how stale values are repaired, and why a measured query needs it. “It might be faster” is not a justification.

## Queries and parameters

A **join** combines related rows:

```sql
SELECT c.code, c.title, e.status
FROM enrollments e JOIN courses c ON c.id = e.course_id
WHERE e.learner_id = ? ORDER BY c.code
```

The `?` is a parameter placeholder. Pass values separately (`execute(sql, (learner_id,))`); never format user input into SQL. An aggregate such as `COUNT(*)` summarizes rows. A lifecycle transition updates one enrollment from `active` to `completed`; the application can check allowed transitions, while a `CHECK` protects values. A history table can preserve every transition if auditability matters.

## Delete behavior and migrations

`CASCADE` deletes dependent rows automatically; `RESTRICT` rejects deletion while dependents exist. Choose based on meaning: deleting a learner may remove disposable enrollment links, while deleting a course with records may need archive/restrict. A **migration** is a repeatable schema change applied in a known order. Test forward migration and a disposable rollback; never experiment on an unverified connection. Existing large tables may require staged nullable columns, backfill, validation, then a constraint.

## Common mistakes

1. Relying on application checks for uniqueness while two writers can race.
2. Forgetting SQLite foreign-key enforcement.
3. Storing a comma-separated course list instead of a relationship table.
4. Using `ON DELETE CASCADE` without considering accidental data loss.
5. Building SQL with f-strings from input.
6. Calling a migration repeatable when it requires manual edits or a specific hidden state.

## Reviewing AI-generated SQL

Review keys, nullability, uniqueness, foreign-key enforcement, check values, delete behavior, indexes, parameterization, and dialect assumptions. Ask whether a migration is reversible and what happens to existing rows. Reject `DROP TABLE`, broad cascades, automatic defaults that invent business data, and denormalization without a source of truth and measured reason.

## Knowledge checks — pause before answers

1. Why does the composite primary key on `enrollments` prevent duplicate membership?
2. What is the difference between a primary key and a foreign key?
3. When might `RESTRICT` be safer than `CASCADE`?
4. Why are SQL parameters safer than string formatting?
5. What makes a duplicate count a denormalization risk?

### Answers

1. The pair `(learner_id, course_id)` must be unique, so a second row for that pair violates the key.
2. A primary key identifies a row in its own table; a foreign key references a row elsewhere and can enforce that it exists.
3. When deleting a parent would erase meaningful history or many unexpected dependents.
4. The database treats the value as data rather than executable SQL syntax.
5. It can disagree with the relationship table unless every write path updates it and a repair strategy exists.

## Notebook preparation

Draw the four entities and cardinalities, list invariants, and use only `sqlite3.connect(':memory:')`. Run the notebook fresh; it creates minimal synthetic rows, runs positive and rejected writes, and demonstrates rollback.

## Summary and next connection

Schema design starts with use cases and invariants, then chooses keys, relationships, constraints, and deletion semantics. Parameterized joins prove the model works; migrations make it reproducible. Next, you will measure how those queries behave and protect concurrent changes.

## A slower walkthrough: turn a use case into tables

Start with the sentence “Ana enrolls in Python.” There are two people/things and one relationship: a learner, a course, and an enrollment. The learner and course each have their own identity. The enrollment needs both identities, a status, and perhaps a date. That is why `enrollments(learner_id, course_id, status)` is a relationship table instead of a column on either parent. A second learner can enroll in the same course, and one learner can enroll in many courses without adding columns.

Write the facts before writing SQL. “A course code is unique” becomes `UNIQUE(code)`. “An enrollment must name a learner” becomes `NOT NULL` plus a foreign key. “One pair can appear once” becomes the composite primary key. “Only three statuses are valid” becomes a `CHECK`. The application can add richer transition rules, but the database should reject impossible values from scripts, tests, and future services too.

### Cardinality with a small drawing

```text
learners 1 ---- many enrollments many ---- 1 courses
```

Read each side separately: one learner may have many enrollment rows; one course may have many enrollment rows. The relationship table turns the many-to-many statement into two one-to-many relationships. A repeated-column design (`course_1`, `course_2`) has no natural answer for the third course and makes joins and constraints awkward.

### Delete behavior is a product decision

If a learner is removed, cascading enrollment links may be acceptable for disposable membership records. If a course has completion history, restricting deletion or marking it archived may be safer. `CASCADE` is not “clean up”; it is permission to remove dependents automatically. `RESTRICT` is not always correct either: an archival policy may require a separate status rather than blocking an administrator forever. Name the business meaning and test the selected behavior.

## Migrations as a conversation with existing data

A migration is not merely a `CREATE TABLE` statement. It runs against data that may already exist. Adding a non-null column without a safe value can fail; adding a unique constraint can reveal duplicates; a destructive drop can erase history. In a large system, stage a new nullable column, backfill and measure, validate, then enforce the final rule. The notebook uses an in-memory database so you can practice forward setup and rollback without touching real data.
