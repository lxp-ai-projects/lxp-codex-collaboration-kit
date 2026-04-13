# Kotlin Spring Boot Developer - version 1.0 - last updated: 2024-06-17 - by Laurie and Patrick

## Purpose

Use this skill to design, implement, review, and refine backend features in Kotlin with Spring Boot.

This skill is meant to support work such as:
- REST API development
- application service design
- validation and error handling
- persistence and repository integration
- authentication and authorization flows
- modular backend architecture
- testable and maintainable feature delivery

The expected outcome is production-conscious backend work that is clear, secure, maintainable, and aligned with documented architecture and project conventions.

---

## Engineering Principles

- align with JetBrains Kotlin best practices where applicable
- apply SRP (Single Responsibility Principle): classes and functions should have focused responsibilities
- apply DRY carefully: remove wasteful duplication, but do not introduce harmful abstraction just to deduplicate superficially
- apply YAGNI: do not build speculative features, abstractions, or extension points without present need
- prefer clean code that is readable, explicit, and intention-revealing
- keep code easy to understand, easy to test, and easy to evolve
- choose clarity over cleverness
- let simplicity survive unless complexity is truly justified

---

## When to Use

Use this skill when:
- the project uses Kotlin and Spring Boot
- backend APIs or services need to be created or modified
- domain, application, infrastructure, or web layers need to be designed or updated
- repository, service, controller, security, or configuration code is involved
- backend testing strategy must be defined or improved
- documentation and architecture impact should be considered alongside backend changes

Do not use this skill when:
- the work is purely frontend
- the task is primarily infrastructure automation unrelated to Spring Boot application code
- the stack is not Kotlin / Spring Boot
- the task is purely product discovery without implementation or backend architecture impact

---

## Assumptions

Default assumptions for this skill:
- the project uses Kotlin with Spring Boot
- code should align with an existing documented architecture when one exists
- secure coding is required by default
- test coverage should reflect feature risk and impact
- major changes should remain traceable to documented requirements or feature scope
- the repository is the source of truth for architecture, standards, and delivery documentation

Unless explicitly stated otherwise:
- use constructor injection
- prefer explicit, readable code over magical abstractions
- keep responsibilities clearly separated
- avoid silent architecture drift
- treat documentation updates as part of the work when relevant

---

## Core Working Principles

- clarify the feature or task before major implementation
- keep changes scoped to the stated objective
- prefer maintainability over unnecessary cleverness
- align code with architectural boundaries
- use Kotlin idiomatically, but not performatively
- favor explicit contracts and predictable behavior
- design for testability
- treat secure coding as normal engineering discipline
- update documentation when the implementation changes the project truth
- surface tradeoffs clearly instead of hiding them in code

---

## Recommended Workflow

1. Clarify the backend objective, scope, and constraints
2. Identify impacted modules, layers, and documentation
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
- controllers handle HTTP concerns, request mapping, response shaping, and validation entry points
- services handle business orchestration and use-case execution
- repositories handle persistence access
- domain logic should not be buried in controllers
- repositories should not become orchestration layers
- configuration should remain focused and explicit
- security logic should be centralized and understandable

Prefer:
- feature-aware organization or clean package boundaries
- focused services
- DTOs for transport boundaries
- explicit mapping between transport and domain/application models
- clear ownership of transactional boundaries
- minimal leakage of framework details into business logic where practical

When relevant, document major architecture impact through ARD or ADR updates.

---

## Kotlin Standards

- prefer immutable `val` over mutable `var` unless mutation is required
- use data classes appropriately for DTO-style models and value carriers
- keep nullability explicit and deliberate
- avoid excessive use of `!!`
- prefer expressive function names over comments that explain unclear code
- use sealed classes or enums when they improve clarity of bounded states
- use extension functions sparingly and only when they improve readability
- avoid overly clever functional chains when a straightforward block is clearer
- prefer `runCatching` over scattered `try/catch` blocks when it improves readability and flow
- avoid verbose exception handling patterns when Kotlin’s result-oriented style provides a clearer alternative
- use `try/catch` explicitly only when boundary handling, recovery behavior, or readability clearly justifies it
- avoid unnecessary `companion object` usage for private constants or private fields
- for private static-like values, prefer top-level private declarations or other simpler constructs when appropriate
- keep coroutine usage explicit and consistent when applicable

---

## Spring Boot Standards

- prefer constructor injection
- keep controllers thin
- validate external input explicitly
- use dedicated request and response models for API boundaries when needed
- avoid leaking persistence entities directly through public API contracts unless intentionally designed
- centralize exception handling when appropriate
- keep configuration typed and explicit
- separate security configuration from business behavior
- avoid hidden side effects in bean configuration
- make transactional behavior intentional, visible, and justifiable

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

## Persistence Expectations

- keep repository responsibilities focused on persistence access
- avoid embedding large amounts of business logic in repository implementations
- model transactions deliberately
- be cautious with lazy loading, N+1 patterns, and hidden database cost
- make data access patterns readable and testable
- document migration or schema impact when relevant
- do not assume persistence details are harmless to API or service design

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
- JUnit 5
- MockK
- Spring Boot Test
- Testcontainers when infrastructure-backed integration testing is needed

For MockK:
- prefer annotation-based setup over manual mock instantiation when appropriate
- use `@MockK` and related annotations for consistency and readability
- keep test setup explicit and maintainable
- avoid overcomplicating tests with unnecessary mocking layers
- test names should reflect the behavior being tested, not the implementation details
- test names should use kotlin backticks for readability when appropriate

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
- API behavior with Spring context involved

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

Testing should reflect real risk, not just satisfy a ritual.

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
- skipping integration tests on risky Spring behavior
- changing architecture without documenting the impact
- adding broad refactors inside a narrowly scoped feature without explicit justification
- relying on verbose `try/catch` blocks where Kotlin result-oriented handling would be clearer
- using `companion object` for private constants or private static-like fields without real justification
- mixing inconsistent mocking styles across the test suite without reason
- using `/* given */`, `/* when */`, `/* then */` comments in unit tests
- assuming that 100% code coverage means the feature is fully tested
- ignoring edge cases because line coverage looks high

---

## Definition of Done

A task using this skill is closer to done when:
- the backend objective is met
- implementation follows Spring Boot and Kotlin conventions
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

---

## Example Prompts

- "Implement a secured Spring Boot endpoint in Kotlin for creating a new customer, with validation, service layering, and integration tests."
- "Review this Kotlin Spring Boot service and identify architecture, testing, and secure coding concerns."
- "Design the backend structure for this feature in Kotlin with Spring Boot, including controller, service, repository, DTOs, and test strategy."
- "Refactor this Spring Boot flow to better separate responsibilities and document any architecture impact."