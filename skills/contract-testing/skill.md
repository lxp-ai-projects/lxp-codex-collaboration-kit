# Contract Testing - version 1.0 - last updated: 2026-04-12 - by Laurie and Patrick

## Purpose

Use this skill to design, implement, review, and refine contract testing practices that keep API contracts and real system behavior aligned.

This skill is meant to support work such as:
- verifying that backend implementations match documented API contracts
- validating request, response, parameter, and error behavior against a shared contract
- protecting frontend and backend integration from silent drift
- supporting contract-first and OpenAPI-first workflows
- strengthening CI validation for API changes
- improving confidence in consumer-visible behavior
- catching compatibility and schema regressions early

The expected outcome is contract validation that is clear, meaningful, maintainable, and aligned with documented API behavior, implementation reality, and consumer expectations.

---

## Engineering Principles

- prefer contract verification over assumption
- treat contracts as executable quality boundaries, not decorative documentation
- prefer explicit drift detection over late discovery
- apply SRP (Single Responsibility Principle): each contract test should validate a coherent contract concern
- apply DRY carefully: reuse validation patterns without obscuring intent
- apply YAGNI: do not build speculative contract-testing infrastructure without present need
- prefer clean, readable, intention-revealing test design
- keep contract tests easy to understand, easy to maintain, and easy to diagnose
- choose clarity over cleverness
- let simplicity survive unless complexity is truly justified

---

## When to Use

Use this skill when:
- the project uses OpenAPI-first or contract-first API design
- backend implementation must be validated against a documented contract
- frontend and backend depend on a shared API contract
- API compatibility and schema regressions must be caught early
- CI should validate contract alignment
- request, response, parameter, or error behavior needs consumer-visible verification
- an API change may affect multiple consumers or integration points

Do not use this skill when:
- the interface being tested does not benefit from a formal contract
- the work is purely frontend with no contract boundary involved
- the task is purely internal implementation validation that does not involve consumer-visible contract behavior
- a lower-level test is sufficient and contract testing would add noise without value

---

## Assumptions

Default assumptions for this skill:
- the repository is the source of truth for API contracts, architecture, and delivery documentation
- secure coding is required by default
- contract behavior should remain explicit and testable
- implementation must not silently drift away from documented API behavior
- tests should reflect consumer-visible behavior, not only internal implementation details
- contract changes should remain traceable to documented requirements or feature scope

Unless explicitly stated otherwise:
- contract testing should support, not replace, unit, integration, and end-to-end testing
- contract tests should focus on the boundary between documented API behavior and real implementation
- request, response, parameter, and error behavior should be validated deliberately
- auth/authz expectations should be validated where they are part of the contract
- contract validation should be compatible with CI quality gates

---

## Core Working Principles

- identify the contract boundary before writing tests
- validate consumer-visible behavior against the documented contract
- treat request, response, parameters, and errors as first-class contract surfaces
- make contract drift visible early
- keep tests focused on contract truth, not incidental implementation detail
- validate non-happy-path behavior as part of the contract when relevant
- keep contract tests diagnosable and maintainable
- update documentation when the contract truth changes
- surface tradeoffs clearly instead of hiding them in tooling or test abstraction

---

## Recommended Workflow

1. Identify the contract source and scope
2. Clarify which consumer-visible behaviors must be validated
3. Identify which contract concerns belong in contract tests rather than unit or general integration tests
4. Implement focused contract validation for requests, responses, parameters, errors, and auth where relevant
5. Review contract drift, compatibility, and schema implications
6. Integrate meaningful checks into CI
7. Refine failures so they are easy to diagnose
8. Update related docs, ADRs, or standards when relevant

---

## Contract Boundary Expectations

- identify what is part of the public contract and what is internal implementation detail
- validate the documented boundary, not hidden internal wiring
- prefer testing the observable API shape and behavior
- do not collapse contract validation into generic “endpoint works” testing
- contract tests should confirm that the system behaves as documented to its consumers
- keep contract scope explicit when only part of an API surface is under validation

---

## OpenAPI and Contract-First Expectations

- contract tests should reinforce contract-first discipline
- use the OpenAPI contract as a validation source when the repository is OpenAPI-first
- ensure request and response behavior remains aligned with the documented schemas
- validate parameter behavior, error behavior, and auth-related responses where they are part of the contract
- contract changes should be explicit, reviewed, and reflected in tests
- major implementation changes should not silently bypass the agreed contract

---

## Request and Response Validation Expectations

- validate request shape expectations deliberately
- validate required vs optional field behavior
- validate nullable vs non-nullable behavior where relevant
- validate response schema shape and important field semantics
- validate status codes intentionally
- validate parameter handling explicitly for path, query, header, and cookie inputs when relevant
- avoid “close enough” contract testing that ignores meaningful schema or behavior drift
- use examples and known consumer expectations to strengthen test relevance where appropriate

---

## Error Contract Expectations

- validate error behavior as part of the contract, not as an afterthought
- verify documented error status codes and envelopes where relevant
- distinguish validation, unauthorized, forbidden, not found, conflict, and server-side failure behavior deliberately
- ensure error payloads do not leak internal implementation details
- keep error validation aligned with documented consumer expectations

---

## Authentication and Authorization Expectations

- validate auth-related contract behavior where it is part of the public API
- verify unauthenticated and unauthorized behavior deliberately
- do not assume happy-path access proves auth contract correctness
- validate token, cookie, session, or permission-related outcomes where relevant
- keep authentication and authorization expectations distinct in tests when they are distinct in the contract

---

## Consumer Compatibility Expectations

- design contract tests with consumer impact in mind
- treat breaking schema or behavior changes as significant
- validate compatibility-sensitive changes deliberately
- ensure contract tests help detect consumer-visible regressions early
- prefer explicit contract evolution over accidental breakage
- use contract tests to protect backend/frontend alignment where shared DTO or client workflows exist

---

## Test Pyramid Expectations

- contract testing sits above isolated unit validation and alongside focused integration validation of boundary behavior
- contract tests should not replace lower-cost testing layers
- use unit tests for internal logic
- use integration tests for component or service interaction
- use contract tests to validate documented boundary behavior
- use end-to-end tests for full user journeys when browser- or client-level confidence is needed
- do not overload contract tests with concerns that belong more clearly to cheaper or broader test layers

---

## Tooling and Execution Expectations

- choose tooling deliberately based on the contract source and repository stack
- keep contract-testing setup understandable
- do not build excessive tooling abstraction without real need
- make test failures readable and actionable
- ensure contract validation can run in CI where it provides meaningful value
- keep generated or supporting validation artifacts understandable when the project uses them
- prefer maintainable validation over tool-driven ceremony

---

## CI and Quality Gate Expectations

- contract tests should support meaningful CI quality gates
- validate contract alignment on pull requests or protected branches where appropriate
- make drift visible before merge when possible
- avoid contract validation that is so brittle or opaque that teams stop trusting it
- treat consumer-visible contract regressions as serious quality concerns
- keep CI feedback clear enough that failures can be diagnosed without guessing

---

## Security Expectations

- validate security-relevant contract behavior where it is part of the API surface
- do not expose internal fields or sensitive details through documented or tested responses carelessly
- validate auth/authz failure behavior when relevant
- ensure error validation does not normalize leakage of internal details
- keep contract tests aligned with secure coding expectations and documented security behavior

---

## Testing Expectations

Testing should validate that contract and implementation remain aligned in meaningful ways.

- validate request and response behavior against the contract
- validate documented parameters and their behavior
- validate documented errors and failure categories
- validate auth-related behavior where relevant
- validate compatibility-sensitive behavior when evolving existing APIs
- use contract tests to detect drift, not to create redundant noise
- 100% implementation coverage does not prove contract correctness
- edge cases and non-happy-path behavior still matter
- contract tests should reflect consumer-visible truth, not internal assumptions

For test structure:
- always use `/* arrange */`, `/* act */`, `/* assert */`
- never use `/* given */`, `/* when */`, `/* then */`

---

## Documentation Expectations

Update documentation when relevant, including:
- OpenAPI specs
- feature docs
- API usage notes
- architecture docs when boundary assumptions change
- ADRs when meaningful contract-testing or compatibility decisions are made
- CI documentation when contract validation becomes part of quality gates
- testing notes when new contract-validation patterns are introduced

Do not let implementation drift away from the documented contract without acknowledgment.

---

## What to Avoid

- treating the contract as passive documentation only
- validating only happy-path responses and calling it contract coverage
- ignoring parameters, errors, or auth behavior that are part of the documented contract
- coupling contract tests tightly to internal implementation details
- overloading contract tests with concerns better handled by unit or full end-to-end tests
- allowing silent schema drift
- treating green implementation tests as proof of contract alignment
- using opaque tooling layers that nobody can debug
- assuming generated clients or DTOs guarantee contract correctness automatically
- ignoring consumer-visible breaking changes until late integration

---

## Definition of Done

A task using this skill is closer to done when:
- the contract boundary is clear
- consumer-visible request, response, parameter, and error behavior were validated appropriately
- auth/authz behavior was validated where relevant
- contract drift risk was addressed explicitly
- compatibility implications were considered
- relevant contract tests were added or updated
- CI integration was considered where appropriate
- relevant documentation was updated
- known tradeoffs, limitations, or follow-ups were made explicit

---

## Example Tasks

- validate that a backend implementation conforms to an OpenAPI-documented listing endpoint
- add contract tests for request validation, response shape, and error handling on a new API feature
- detect and prevent drift between an OpenAPI spec and backend behavior
- add contract validation to CI for a contract-first repository
- review whether a schema change is backward compatible for consumers
- validate auth-related contract behavior for protected endpoints
- align frontend and backend teams around executable contract checks

---

## Example Prompts

- "Design a contract-testing strategy for this OpenAPI-first API, including request, response, parameter, error, and auth validation."
- "Review this backend feature and identify which behaviors should be validated through contract tests versus lower or higher test layers."
- "Help me add contract validation to CI so schema or behavior drift is caught before merge."
- "Evaluate whether this API change is consumer-safe and how contract tests should reflect it."