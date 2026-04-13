# API Designer OpenAPI - version 1.1 - last updated: 2026-04-12 - by Laurie and Patrick

## Purpose

Use this skill to design, review, and refine APIs using an OpenAPI-first, contract-first approach.

This skill is meant to support work such as:
- REST API contract design
- request and response modeling
- endpoint and resource design
- error contract definition
- authentication and authorization documentation
- backend/frontend integration alignment
- API versioning and compatibility thinking
- documentation-first collaboration

The expected outcome is an API contract that is clear, explicit, secure, testable, and usable as a shared source of truth across product, backend, frontend, QA, and documentation work.

---

## Engineering Principles

- prefer contract-first design over implementation-led drift
- make API behavior explicit before coding major flows
- design for clarity, consistency, and consumer usability
- apply SRP (Single Responsibility Principle): each endpoint and schema should have a clear purpose
- apply DRY carefully: reuse schema components when it reduces repetition without obscuring meaning
- apply YAGNI: do not model speculative endpoints, fields, or flows without present need
- prefer clean, readable, intention-revealing API contracts
- keep contracts easy to understand, easy to validate, and easy to evolve
- choose clarity over cleverness
- let simplicity survive unless complexity is truly justified

---

## When to Use

Use this skill when:
- a new API is being designed
- an existing API is being extended or refactored
- frontend and backend need a shared contract
- API documentation should act as a source of truth
- request, response, error, or auth behavior needs to be modeled clearly
- versioning, compatibility, or deprecation concerns must be considered
- the team wants implementation to follow an explicit OpenAPI contract

Do not use this skill when:
- the work is purely internal and does not benefit from an explicit API contract
- the task is purely frontend with no API design implications
- the work is purely infrastructure automation unrelated to API design
- the problem requires a different interface style and OpenAPI is not an appropriate fit

---

## Assumptions

Default assumptions for this skill:
- the API contract should be written and reviewed before major implementation
- the repository is the source of truth for architecture, standards, and delivery documentation
- secure coding is required by default
- API behavior should be explicit and testable
- contracts should remain aligned with implementation
- major API changes should remain traceable to documented requirements or feature scope

Unless explicitly stated otherwise:
- use OpenAPI as the contract format
- prefer OpenAPI 3.1 unless the project explicitly standardizes on another supported version
- design RESTful APIs with explicit request and response schemas
- document authentication and authorization expectations clearly
- use explicit examples where they improve consumer understanding
- treat error contracts as first-class API behavior
- consider backward compatibility when changing existing endpoints
- avoid silent contract drift after implementation

---

## Core Working Principles

- clarify the use case before designing the endpoint
- design contracts around real consumer needs, not internal implementation structure
- keep endpoint behavior explicit
- keep schemas readable and intentional
- model errors deliberately
- document auth and permission expectations clearly
- treat contract design as a collaboration tool, not just a documentation artifact
- update documentation when API truth changes
- surface tradeoffs clearly instead of hiding them in the implementation
- prefer stability and predictability over clever endpoint design

---

## Recommended Workflow

1. Clarify the use case, actors, and expected behavior
2. Identify the resource or interaction model
3. Define endpoint paths, methods, and intent
4. Design request, response, parameter, and error schemas
5. Define auth/authz expectations
6. Review compatibility, naming, consistency, and consumer ergonomics
7. Validate examples and consumer usability
8. Implement against the contract
9. Update docs, tests, and related ADRs when relevant

---

## Contract-First Expectations

- define the API contract before major implementation
- use the OpenAPI spec as a collaboration artifact between backend, frontend, QA, and documentation
- avoid designing the contract as a reverse-engineered afterthought from code
- treat the contract as part of the product and engineering design
- major endpoint implementation should not start before the contract has been reviewed and accepted
- backend and frontend should align on the contract before implementation drift begins
- make meaningful API changes visible in documentation and review
- ensure implementation follows the contract or update the contract explicitly

---

## Resource and Endpoint Design Expectations

- use clear, stable, and intention-revealing endpoint names
- prefer resource-oriented design where appropriate
- keep endpoint responsibilities focused
- avoid collapsing unrelated actions into a single unclear endpoint
- use HTTP methods deliberately
- distinguish between collection, resource, and action semantics clearly
- avoid path naming that leaks unstable implementation details
- prefer consistency across similar endpoints
- design with consumer readability in mind

---

## Request and Response Modeling Expectations

- define request and response schemas explicitly
- model path, query, header, and cookie parameters explicitly when they are part of the contract
- use reusable schema components where they reduce real duplication
- do not force reuse when separate schemas are clearer
- model required vs optional fields deliberately
- model nullable fields deliberately
- keep payloads intention-revealing and bounded
- avoid returning internal-only fields carelessly
- avoid ambiguous shapes that are hard to validate or consume
- include examples when they materially improve understanding
- keep transport models separate from internal implementation concerns where relevant

---

## Consumer and Generation Expectations

- design schemas so they remain understandable for both humans and tooling
- avoid ambiguous unions or loosely typed structures unless they are truly necessary
- keep enum values explicit and stable
- model nullable and optional fields deliberately
- prefer contracts that can support generated clients or shared DTO workflows cleanly when the project needs them
- do not let generator convenience override contract clarity, but do consider consumer ergonomics seriously
- request and response contracts should map cleanly to explicit DTOs
- distinguish transport schemas from persistence models
- avoid contract ambiguity that creates fragile mapper logic in strongly typed backends
- contracts should support explicit DTO validation at the framework boundary when used in typed backend frameworks such as Kotlin/Spring Boot or NestJS

---

## Error Contract Expectations

- treat error responses as part of the public contract
- define error shapes intentionally
- keep error responses consistent across the API where practical
- define a consistent error envelope when the project uses one
- avoid leaking internal implementation details, stack traces, or infrastructure specifics
- distinguish validation, authorization, not found, conflict, and server failure cases deliberately
- document relevant status codes and their meanings clearly
- ensure consumers can distinguish technical failure from validation, auth, authorization, conflict, and not-found behavior
- ensure consumers can understand what category of error occurred without reverse-engineering the backend

---

## Authentication and Authorization Expectations

- document authentication requirements explicitly
- document authorization expectations explicitly
- do not assume auth behavior is obvious to consumers
- indicate which endpoints require auth and which do not
- indicate role, scope, or permission expectations where relevant
- document cookie, token, or session expectations when relevant
- ensure auth-related failure responses are modeled clearly
- treat authentication and authorization as separate concerns in the contract

---

## Versioning and Compatibility Expectations

- consider compatibility before changing existing endpoints
- prefer additive evolution when possible
- document breaking changes explicitly
- avoid casual breaking changes to widely used contracts
- define deprecation behavior deliberately when relevant
- ensure versioning strategy is understandable and consistent
- keep consumers in mind when introducing field or behavior changes

---

## Pagination, Filtering, and Query Expectations

- design pagination explicitly when listing resources
- keep filtering and sorting parameters clear and bounded
- avoid ad hoc parameter sprawl
- define default behavior where relevant
- document expected query parameter shapes clearly
- keep pagination metadata understandable
- ensure list behavior is predictable for consumers

---

## Security Expectations

- do not expose sensitive internal fields by default
- validate boundary assumptions in request models
- document auth/authz expectations clearly
- avoid over-permissive contract design
- be careful with file upload, token, cookie, and sensitive data flows
- design error contracts that do not leak internal details
- consider abuse, enumeration, replay, and access control risks where relevant
- make security-relevant behavior visible in the contract and related docs

---

## OpenAPI Structure Expectations

- keep the spec readable and organized
- prefer OpenAPI 3.1 unless the project explicitly standardizes on another supported version
- use `components` deliberately
- define `operationId` values consistently
- use tags meaningfully and group them by domain or bounded feature area
- avoid excessive indirection in schema references
- keep paths, schemas, parameters, and examples easy to navigate
- keep naming conventions consistent
- avoid duplicating near-identical schemas unless clarity truly benefits
- prefer maintainable structure over clever spec gymnastics

---

## Testing Expectations

Testing should validate that implementation and contract remain aligned.

- validate that request and response behavior matches the contract
- validate error behavior against the documented contract
- validate auth-related behavior against documented expectations
- validate pagination, filtering, and compatibility-sensitive flows when relevant
- treat contract conformance as a real quality concern
- 100% implementation coverage does not prove contract correctness
- edge cases and non-happy-path behavior must still be considered
- API tests should reflect consumer-visible behavior, not only backend internals

For test structure:
- always use `/* arrange */`, `/* act */`, `/* assert */`
- never use `/* given */`, `/* when */`, `/* then */`

---

## Documentation Expectations

Update documentation when relevant, including:
- OpenAPI specs
- feature docs
- PRD sections impacted by API behavior changes
- architecture docs when API boundaries or interaction models change
- ADRs when meaningful contract or versioning decisions are made
- authentication and integration notes
- setup or consumer usage notes when relevant

Do not let implementation drift away from the documented contract without acknowledgment.

---

## What to Avoid

- designing the API from internal class structure instead of consumer need
- treating OpenAPI as a reverse-generated artifact only
- vague or inconsistent endpoint naming
- ambiguous request or response shapes
- undocumented error behavior
- undocumented auth/authz expectations
- leaking internal implementation details in contracts
- casual breaking changes
- path or schema naming drift across similar endpoints
- overabstracting the spec until it becomes hard to read
- assuming implementation coverage proves contract quality
- ignoring consumer usability when designing the contract
- designing contracts that encourage exposing persistence entities directly
- leaving parameters, examples, or auth expectations implicit when they materially affect consumption

---

## Definition of Done

A task using this skill is closer to done when:
- the API use case is clearly modeled
- endpoint responsibilities are understandable
- request, response, parameter, and error contracts are explicit
- auth/authz expectations are documented
- compatibility implications were considered
- security-sensitive aspects were considered
- implementation and contract are aligned
- relevant tests were added or updated
- relevant documentation was updated
- known tradeoffs, limitations, or follow-ups were made explicit

---

## Example Tasks

- design a contract-first REST API for a new feature before backend implementation begins
- define pagination, filtering, and error contracts for a listing endpoint
- add authentication and authorization details to an OpenAPI specification
- review an API spec for clarity, compatibility, and consumer usability
- refactor an existing API contract to improve consistency and schema readability
- document a breaking API change and its versioning implications
- align frontend and backend teams around a shared OpenAPI contract
- design request/response schemas that map cleanly to explicit DTOs in Kotlin/Spring Boot or NestJS

---

## Example Prompts

- "Design an OpenAPI-first contract for this feature, including endpoints, schemas, parameters, error responses, and auth expectations."
- "Review this OpenAPI spec for clarity, consistency, security, consumer usability, and backward compatibility concerns."
- "Help me refactor this API contract so it is more consumer-friendly, DTO-friendly, and easier to maintain."
- "Model pagination, filtering, parameters, and error handling for this REST endpoint in a contract-first way."