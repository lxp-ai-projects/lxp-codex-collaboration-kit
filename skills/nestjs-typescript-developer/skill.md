# NestJS TypeScript Developer - version 1.0 - last updated: 2026-04-12 - by Laurie and Patrick

## Purpose

Use this skill to design, implement, review, and refine backend features in NestJS with TypeScript.

This skill is meant to support work such as:
- REST API development
- application service design
- validation and error handling
- persistence and repository integration
- authentication and authorization flows
- modular backend architecture
- testable and maintainable feature delivery
- lightweight but production-conscious backend development

The expected outcome is production-conscious backend work that is clear, secure, maintainable, and aligned with documented architecture and project conventions.

---

## Engineering Principles

- align with NestJS and TypeScript best practices where applicable
- apply SRP (Single Responsibility Principle): modules, services, controllers, repositories, and utilities should have focused responsibilities
- apply DRY carefully: remove wasteful duplication, but do not introduce harmful abstraction just to deduplicate superficially
- apply YAGNI: do not build speculative features, abstractions, or extension points without present need
- prefer clean code that is readable, explicit, and intention-revealing
- keep code easy to understand, easy to test, and easy to evolve
- choose clarity over cleverness
- let simplicity survive unless complexity is truly justified

---

## When to Use

Use this skill when:
- the project uses NestJS with TypeScript
- backend APIs or services need to be created or modified
- module, controller, service, repository, guard, interceptor, or configuration code is involved
- backend testing strategy must be defined or improved
- documentation and architecture impact should be considered alongside backend changes
- a lightweight but structured backend is preferred over a heavier enterprise stack

Do not use this skill when:
- the work is purely frontend
- the task is primarily infrastructure automation unrelated to NestJS application code
- the stack is not NestJS / TypeScript
- the task is purely product discovery without implementation or backend architecture impact

---

## Assumptions

Default assumptions for this skill:
- the project uses NestJS with TypeScript
- the project should use a current NestJS version approved and supported by the project
- the project should use a current Node.js LTS version approved and supported by the project
- the project must make an explicit persistence choice between MongoDB and SQL
- when SQL is selected, PostgreSQL is the recommended default unless another relational database is explicitly required
- the project may use Redis or Valkey as supporting infrastructure when caching, ephemeral state, token management, rate limiting, coordination, or similar needs justify it
- code should align with an existing documented architecture when one exists
- secure coding is required by default
- test coverage should reflect feature risk and impact
- major changes should remain traceable to documented requirements or feature scope
- the repository is the source of truth for architecture, standards, and delivery documentation

Unless explicitly stated otherwise:
- use TypeScript everywhere
- do not use `any`
- prefer explicit, readable code over magical abstractions
- keep responsibilities clearly separated
- avoid silent architecture drift
- treat documentation updates as part of the work when relevant
- containerization should be considered part of production-conscious delivery when relevant

---

## Core Working Principles

- clarify the feature or task before major implementation
- keep changes scoped to the stated objective
- prefer maintainability over unnecessary cleverness
- align code with architectural boundaries
- use NestJS idiomatically, but not performatively
- favor explicit contracts and predictable behavior
- design for testability
- treat secure coding as normal engineering discipline
- update documentation when the implementation changes the project truth
- surface tradeoffs clearly instead of hiding them in code

---

## Recommended Workflow

1. Clarify the backend objective, scope, and constraints
2. Identify impacted modules, controllers, services, repositories, guards, and documentation
3. Check architecture, conventions, and existing patterns
4. Propose the implementation approach before large changes
5. Implement in scoped, traceable steps
6. Refine naming, error handling, and boundary clarity
7. Add or update the appropriate tests
8. Update related docs, ADRs, or standards when relevant

---

## Architecture and Design Expectations

Prefer clear layered responsibilities.

Typical boundary expectations:
- controllers handle HTTP concerns, request mapping, request/response shaping, and boundary validation entry points
- services handle business orchestration and use-case execution
- repositories or dedicated data-access layers handle persistence access
- guards handle access control concerns
- interceptors, pipes, and filters should remain focused on cross-cutting or boundary-level responsibilities
- domain logic should not be buried in controllers
- repositories should not become orchestration layers
- configuration should remain focused and explicit
- security logic should be centralized and understandable

Prefer:
- feature-aware organization or clean module boundaries
- focused services
- DTOs for transport boundaries
- explicit mapping between transport and domain/application models
- clear ownership of transactional boundaries
- minimal leakage of framework details into business logic where practical

When relevant, document major architecture impact through ARD or ADR updates.

---

## TypeScript Standards

- use TypeScript throughout the codebase
- do not use `any`
- prefer explicit types and intention-revealing contracts
- use interfaces, types, enums, and discriminated unions deliberately when they improve clarity
- keep nullability and optionality explicit
- prefer expressive function and method names over comments that explain unclear code
- avoid overly clever functional chains when a straightforward block is clearer
- avoid large files that mix unrelated responsibilities
- keep async flows explicit and understandable
- prefer small, focused utilities over giant generic helper bags

---

## NestJS Standards

- prefer explicit module boundaries
- keep controllers thin
- validate external input explicitly
- use dedicated request and response DTOs at API boundaries when needed
- avoid leaking persistence entities directly through public API contracts unless intentionally designed
- centralize exception handling when appropriate
- keep configuration typed and explicit
- separate security configuration from business behavior
- use guards, interceptors, pipes, and filters deliberately rather than reflexively
- avoid hidden side effects in module wiring
- make transactional behavior intentional, visible, and justifiable

---

## Containerization Standards

When containerization is part of the delivery scope:
- provide a clear and production-conscious Dockerfile
- use a current Node.js LTS runtime approved and supported by the project unless the project explicitly defines another target
- prefer multi-stage builds when they improve final image quality and delivery hygiene
- keep runtime images minimal and explicit
- avoid baking secrets into images
- expose only what is needed
- keep container behavior predictable and environment-driven
- make health, configuration, and startup behavior understandable
- document container assumptions when relevant

When relevant:
- ensure the application runs cleanly in Docker
- ensure external configuration is handled through environment variables or secure runtime configuration
- ensure database and infrastructure dependencies are clearly documented for local and delivery usage

---

## API Design Expectations

- use clear and stable endpoint naming
- keep request and response contracts explicit
- return appropriate HTTP status codes
- design error responses intentionally
- avoid leaking internal implementation details in error payloads
- validate request bodies, parameters, and path inputs
- document authorization expectations clearly
- think about backward compatibility when modifying existing endpoints

If the task affects API behavior, reflect the impact in docs and tests.

---

## Persistence and Supporting Data Infrastructure

The project must make an explicit primary persistence choice based on real product and architecture needs.

Supported primary persistence options:
- MongoDB for document-oriented persistence
- SQL, with PostgreSQL as the recommended default when relational persistence is selected

Supported complementary data infrastructure:
- Redis or Valkey for caching, ephemeral state, token-related workflows, rate limiting, lightweight coordination, or similar supporting concerns

### Choosing Between MongoDB and SQL

Choose MongoDB when:
- the domain is document-oriented
- denormalized read shapes are a good fit
- schema flexibility is valuable
- aggregate-style access patterns dominate
- relational joins are not a core requirement

Choose SQL / PostgreSQL when:
- the domain has strong relational structure
- transactional integrity is important
- joins and relational querying are central
- the data model benefits from stricter structure and constraints
- reporting and relational consistency matter

Do not choose MongoDB or SQL by habit alone.
The persistence model should fit the real domain, access patterns, consistency needs, and operational constraints.

### Relational Persistence

When the project uses SQL:
- PostgreSQL is the recommended default unless another relational database is explicitly required
- prefer TypeORM unless another ORM or lower-level approach is explicitly justified
- keep entity modeling deliberate and readable
- avoid leaking TypeORM entities directly through public API contracts unless intentionally designed
- be careful with relations, eager/lazy loading, cascade behavior, and hidden persistence cost
- model transactional boundaries intentionally
- keep repository responsibilities focused on persistence access
- document schema and migration impact when relevant

### Mongo Persistence

When the project uses MongoDB:
- prefer Mongoose through `@nestjs/mongoose` unless another approach is explicitly justified
- model document structures intentionally
- avoid treating MongoDB as schemaless chaos
- keep repository or data-access responsibilities focused and explicit
- validate assumptions about document shape, indexing, and query behavior
- be explicit about consistency, update patterns, and denormalization tradeoffs
- document collection and index impact when relevant
- keep Mongoose schemas, model usage, and persistence boundaries understandable and maintainable

### Redis / Valkey Usage

When Redis or Valkey is used:
- treat it as supporting infrastructure unless the architecture explicitly defines another role
- be explicit about what data is ephemeral versus authoritative
- do not silently move source-of-truth business state into Redis or Valkey
- document TTL, invalidation strategy, and fallback behavior when relevant
- validate consistency assumptions between cache and primary persistence
- be explicit when Redis or Valkey is used for token blacklisting, session support, rate limiting, caching, or distributed coordination
- document operational impact when relevant

### General Expectations

- keep business logic out of repositories
- make persistence and supporting data choices visible in documentation and ADRs when they materially affect the architecture
- do not assume persistence details are harmless to API, service, performance, or security design
- review indexing, migrations, and operational impact as part of production-conscious delivery

---

## Secure Coding Expectations

At minimum:
- validate all external input
- do not trust client-provided state
- enforce authentication and authorization explicitly
- apply least privilege
- avoid hardcoded secrets
- avoid logging sensitive data
- protect tokens, credentials, and internal system details
- consider broken access control risks whenever adding or modifying endpoints
- consider injection risks in persistence, queries, and dynamic behavior
- fail safely when validation or authorization fails
- avoid exposing stack traces or internal details in public API responses

For security-sensitive features, explicitly review:
- auth/authz paths
- token or session handling
- trust boundaries
- role checks
- input validation coverage
- audit and logging expectations

---

## Testing Expectations

### Testing Stack Preferences

Preferred defaults:
- Jest
- Nest testing utilities
- integration testing with real application wiring where appropriate
- Testcontainers when infrastructure-backed integration testing is needed

For unit tests:
- keep mocks explicit and maintainable
- test names should reflect the behavior being tested, not the implementation details

For test structure:
- always use `/* arrange */`, `/* act */`, `/* assert */`
- never use `/* given */`, `/* when */`, `/* then */`
- `given/when/then` is considered less clear in this context and too closely tied to Cucumber / BDD-style conventions
- test phases should remain immediately readable and explicit

Testing should reflect real risk, not just satisfy a ritual.

High code coverage does not guarantee that a feature is fully tested.
100% coverage can still miss:
- edge cases
- failure paths
- invalid input scenarios
- authorization problems
- business rule gaps
- regression-prone behaviors

Coverage is only one signal.
Tests should be designed to validate meaningful behavior, including edge cases and non-happy-path scenarios.

### Unit Tests
Use for:
- business rules
- validators
- mappers
- utility logic
- focused service logic with mocked dependencies where appropriate

### Integration Tests
Use for:
- controller behavior
- request validation
- persistence interactions
- repository behavior
- security configuration behavior
- service plus infrastructure wiring
- API behavior with real Nest application wiring where appropriate

### Functional / End-to-End Tests
Use when relevant for:
- authentication flows
- critical end-to-end API workflows
- full-stack user-critical scenarios
- regression-prone backend flows exercised through real interfaces

Also validate:
- invalid input
- unauthorized and forbidden access
- empty states
- not found paths
- duplicate or conflicting operations
- failure modes with meaningful error behavior

---

## Documentation Expectations

Update documentation when relevant, including:
- feature docs
- PRD sections impacted by behavior changes
- architecture docs when boundaries or flows change
- ADRs when a meaningful technical decision is made
- API documentation
- setup or operational notes
- testing or security standards if the change introduces new patterns

Do not let backend implementation drift away from the documented project truth without acknowledgment.

---

## What to Avoid

- writing controllers that contain business logic
- mixing persistence concerns with transport concerns
- overengineering simple features
- introducing abstractions before they are justified
- hiding tradeoffs in framework magic
- using unclear names for services, methods, or models
- exposing internal entities carelessly
- treating security as a later concern
- skipping integration tests on risky NestJS behavior
- changing architecture without documenting the impact
- adding broad refactors inside a narrowly scoped feature without explicit justification
- using `any`
- mixing inconsistent mocking styles across the test suite without reason
- using `/* given */`, `/* when */`, `/* then */` comments in unit tests
- assuming that 100% code coverage means the feature is fully tested
- ignoring edge cases because line coverage looks high

---

## Definition of Done

A task using this skill is closer to done when:
- the backend objective is met
- implementation follows NestJS and TypeScript conventions
- responsibilities remain clear across layers
- security-sensitive aspects were considered
- appropriate tests were added or updated
- test coverage is meaningful, not just numerically high
- important edge cases and failure paths were considered
- API and persistence implications were handled deliberately
- relevant documentation was updated
- known limitations or follow-ups were made explicit

---

## Example Tasks

- implement a login endpoint with JWT-based authentication
- add a refresh token flow with revocation support
- create a paginated REST endpoint for resource listing
- add validation and error handling for a new form submission API
- refactor a service to separate orchestration from persistence concerns
- introduce a new secured admin endpoint with role checks
- document and implement a backend feature based on PRD and ADR inputs
- design a persistence strategy and justify whether MongoDB or PostgreSQL is the better fit
- implement a PostgreSQL-backed NestJS feature using TypeORM
- implement a MongoDB-backed NestJS feature using Mongoose and `@nestjs/mongoose`
- introduce Redis or Valkey for caching, token blacklisting, session support, or rate limiting where justified
- containerize a NestJS application with a production-conscious Dockerfile

---

## Example Prompts

- "Design a NestJS persistence strategy and justify whether MongoDB or PostgreSQL is the better fit, including repository structure, transaction considerations, and documentation impact."
- "Implement a PostgreSQL-backed NestJS feature using TypeORM, with validation, service layering, and integration tests."
- "Implement a MongoDB-backed NestJS feature using Mongoose and `@nestjs/mongoose`, with clear document modeling and integration tests."
- "Containerize this NestJS application with a production-conscious Dockerfile."
- "Review whether Redis or Valkey should be introduced for caching, token blacklisting, session support, or rate limiting."