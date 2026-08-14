# Industry-Ready Developer Curriculum

Designed for a junior developer working in an environment where AI writes a lot of the code, but the engineer still needs to **understand, review, debug, and own the system**.

## 1. Code Structure &amp; Maintainability

**Learn**

- Functions, modules, classes, and objects
- Composition vs inheritance
- Separation of concerns
- Dependency injection
- Coupling and cohesion
- DRY, KISS, YAGNI
- Recognizing over-engineered AI-generated code
- Refactoring without changing behavior

**Lab:** Start with a messy API where routes, database logic, and business logic are mixed together. Refactor it into maintainable components.

---

## 2. HTTP &amp; API Design

**Learn**

- Request/response lifecycle
- HTTP methods
- Status codes
- Headers
- Path vs query parameters
- REST conventions
- Pagination and filtering
- Idempotency
- API versioning
- OpenAPI/Swagger
- Backward compatibility

**Lab:** Design and build a small production-style REST API, then identify and fix deliberately bad API design.

---

## 3. Authentication &amp; Authorization

**Learn**

- Authentication vs authorization
- Password hashing
- Sessions vs tokens
- JWTs
- Access and refresh tokens
- Token expiry and revocation
- Role-based access control
- Permissions
- Resource ownership

**Lab:** Progress through:

```text
No authentication
→ Authentication
→ Authorization
→ Ownership rules
→ Refresh tokens
→ Revocation

```

This matches the useful progression already used in the existing Dev Skills Lab.

---

## 4. API Validation &amp; Data Contracts

**Learn**

- Request validation
- Response schemas
- Required and optional fields
- Type validation
- Nested schemas
- Enum validation
- Rejecting unknown fields
- Serialization/deserialization
- Pydantic/Zod-style models
- Consistent API errors

**Lab:** Start with an API accepting arbitrary JSON and progressively make invalid states impossible to submit.

---

## 5. SQL &amp; Database Schema Design

**Learn**

- Tables
- Primary and foreign keys
- Relationships
- Constraints
- Normalization
- Joins
- Migrations
- Referential integrity
- When denormalization makes sense

**Lab:** Design the database for a real application such as an LMS, order-processing system, or document-processing platform.

---

## 6. Database Performance &amp; Transactions

**Learn**

- Indexes
- Composite indexes
- Query plans
- `EXPLAIN`
- N+1 queries
- Connection pooling
- Transactions
- ACID
- Race conditions
- Locking
- Deadlocks
- Optimistic concurrency

**Lab:** Diagnose a slow API endpoint, inspect the query plan, fix the database bottleneck, then simulate two users modifying the same record concurrently.

---

## 7. Error Handling &amp; Resilience

**Learn**

- Expected vs unexpected errors
- Custom error types
- Error propagation
- Centralized error handlers
- Safe client-facing errors
- Timeouts
- Retries
- Exponential backoff
- Circuit breakers
- Graceful degradation
- Idempotency

**Lab:** Introduce API failures, database failures, timeouts, and malformed data. Make the application respond correctly to each.

---

## 8. Testing Production Code

**Learn**

- Unit tests
- Integration tests
- End-to-end tests
- Regression tests
- Fixtures
- Mocks, stubs, and fakes
- What should and shouldn't be mocked
- Testing failure paths
- Test coverage
- Testing database-backed APIs

**Lab:** Take an AI-generated feature and prove whether it actually works by writing tests designed to break it.

---

## 9. Async Processing, Queues &amp; Background Jobs

**Learn**

- Synchronous vs asynchronous execution
- `async/await`
- Workers
- Job queues
- Producers and consumers
- SQS/RabbitMQ concepts
- Retry queues
- Dead-letter queues
- Duplicate delivery
- Idempotent workers

**Lab:** Convert a slow API operation from:

```text
Request → 60-second task → Response

```

into:

```text
Request
→ Queue
→ Worker
→ Result

```

Then handle worker crashes and duplicate jobs.

---

## 10. Logging, Monitoring &amp; Tracing

**Learn**

- Structured logging
- Log levels
- Request IDs
- Metrics
- Latency
- Error rate
- Throughput
- Health checks
- Distributed traces
- Spans
- Trace IDs
- Root-cause debugging from telemetry

**Lab:** Trace one request through several services and a database, then diagnose an intentionally introduced production failure.

---

## 11. Security for Developers

**Learn**

- Broken access control
- SQL injection
- Command injection
- XSS
- CSRF
- SSRF
- Mass assignment
- Path traversal
- Secret leakage
- Dependency vulnerabilities
- Least privilege
- Secure configuration

**Lab:** Build or use an intentionally vulnerable application, exploit the vulnerabilities locally, then fix them.

---

## 12. Docker, Environments &amp; CI/CD

**Learn**

- Containers vs images
- Dockerfiles
- Docker Compose
- Ports
- Volumes
- Environment variables
- Development vs staging vs production
- Secrets
- GitHub Actions
- Build pipelines
- Automated testing
- Deployment
- Rollbacks

**Lab:** Containerize an API with PostgreSQL and Redis, then build:

```text
Pull Request
→ Lint
→ Tests
→ Build
→ Deploy

```

---

## 13. Scalability &amp; Production System Design

**Learn**

- Vertical vs horizontal scaling
- Stateless services
- Load balancing
- Caching
- Redis
- Rate limiting
- Database bottlenecks
- Service boundaries
- Failure domains
- Performance profiling
- Latency vs throughput
- Capacity thinking

**Lab:** Take a simple application and reason through what breaks at:

```text
10 users
1,000 users
100,000 users

```

The goal isn't FAANG interview puzzles. It is recognizing realistic production bottlenecks.

---

## 14. Debugging &amp; AI-Generated Code Review

This should be one of the most important modules.

**Learn**

- Reproducing bugs
- Reading unfamiliar code
- Following data flow
- Using logs and traces
- Forming and testing hypotheses
- Root-cause analysis
- Reading stack traces
- Reviewing diffs
- Spotting hallucinated APIs
- Spotting missing edge cases
- Detecting unnecessary abstractions
- Verifying AI-generated fixes

**Lab:** Give an AI a realistic bug report, let it propose a fix, and review the result instead of trusting it. Require tests proving the root cause is gone.

---

# AI Engineering Extension

Once those foundations are comfortable:

## 15. LLM API Engineering

Model APIs, streaming, rate limits, timeouts, retries, structured outputs, token usage, latency, and cost.

## 16. Tool Calling &amp; Agent Architecture

Tool schemas, agent loops, state, routing, permissions, termination conditions, and failure recovery.

## 17. RAG &amp; Retrieval

Embeddings, chunking, vector search, metadata filtering, hybrid retrieval, reranking, and retrieval evaluation.

## 18. AI Observability &amp; Evaluation

LLM traces, model/tool spans, token and cost tracking, eval datasets, regression testing, LLM-as-judge, task-success metrics, and prompt/model versioning.

---

## Recommended order

```text
Code Structure
      ↓
HTTP & APIs
      ↓
Auth
      ↓
Validation
      ↓
SQL
      ↓
Database Performance
      ↓
Errors & Resilience
      ↓
Testing
      ↓
Async & Queues
      ↓
Observability
      ↓
Security
      ↓
Docker & CI/CD
      ↓
Scalability
      ↓
Debugging & Code Review
      ↓
AI Engineering

```

