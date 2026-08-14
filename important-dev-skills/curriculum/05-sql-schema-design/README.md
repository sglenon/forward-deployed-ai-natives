# Module 5: SQL and database schema design

## Outcome

Design a relational schema that represents the business rules and protects data integrity independently of application code.

## Lab progression

1. Model an LMS enrollment, order workflow, or document-processing system from named use cases.
2. Identify entities, keys, relationships, cardinality, and lifecycle.
3. Normalize repeated data and separate many-to-many relationships.
4. Add primary, foreign, unique, check, and nullability constraints.
5. Write joins that answer required product questions.
6. Apply the schema through versioned migrations.
7. Evaluate one justified denormalization against its consistency cost.

## Required evidence

- An entity-relationship diagram tied to actual queries and rules.
- Migration up and rollback evidence in a disposable database.
- Tests showing constraints reject orphaned, duplicate, and invalid data.
- Example queries for one detail view, one aggregate, and one lifecycle transition.

## Pass conditions

- Keys and constraints encode named business invariants.
- Relationship tables and delete behavior are explicit.
- Migrations are repeatable and do not depend on manual edits.
- The learner can explain what the database guarantees and what remains in application logic.
- Any denormalization has an owner and synchronization strategy.
