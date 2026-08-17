# Module 5: SQL and database schema design

## Start here

A relational database stores related facts in tables. A **schema** is the table/column/constraint design. You will use Python's `sqlite3` with `:memory:` only to design an LMS enrollment schema: learners enroll in courses, courses have sections, and enrollments have a lifecycle. SQL constraints are executable promises that protect data even when application code is bypassed.

You should know basic Python and Module 4's data-boundary ideas. The notebook creates and destroys its own synthetic database; never substitute a production connection.

## Vocabulary preview

- **Schema:** the designed tables, columns, keys, and constraints of a database.
- **Primary key:** a value or combination that uniquely identifies a row.
- **Foreign key:** a reference that can require a related row to exist.
- **Cardinality:** how many rows may relate to another row.
- **Constraint:** a database rule that rejects invalid data.
- **Normalization:** storing each changing fact in one appropriate place.
- **Migration:** a repeatable, ordered change to a schema.

The full [lesson](LESSON.md) turns an enrollment use case into these structures.

## What you will know and do

- explain tables, rows, columns, primary/foreign keys, cardinality, and many-to-many relationship tables;
- use `NOT NULL`, `UNIQUE`, `CHECK`, and foreign-key enforcement for named invariants;
- write parameterized joins, aggregates, lifecycle queries, and repeatable migrations;
- choose cascade/restrict behavior and distinguish normalized source-of-truth data from justified denormalization;
- review AI SQL for missing constraints, unsafe cascades, dialect assumptions, and destructive edits.

## Study order and time

Read [LESSON.md](LESSON.md), draw the entities before opening [lab.ipynb](lab.ipynb), and run the notebook from a fresh kernel. Plan 90–150 minutes.

## Completion checklist

- [ ] I named invariants before writing SQL.
- [ ] I tested duplicate membership, orphan references, invalid statuses, missing fields, and delete behavior.
- [ ] I ran a detail join, aggregate, and lifecycle query with parameters.
- [ ] I can recreate the schema and roll it back in a disposable database.
- [ ] I separated database guarantees from application-only rules.
- [ ] I justified (or rejected) one denormalization and reviewed AI SQL.

## Evidence and pass conditions

Keep the use cases, ER sketch, cardinality/invariant table, migration output, positive/negative checks, query results, delete behavior, dialect assumptions, and AI diff. Pass means constraints encode the named invariants, joins/lifecycle queries are correct, migrations are repeatable, and no denormalized value lacks a source of truth and stale-data plan.

## Next module

Continue to [Module 6: Database performance and transactions](../06-database-performance-transactions/README.md), where you will measure queries and protect concurrent updates.
