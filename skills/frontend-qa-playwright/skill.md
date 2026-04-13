# Frontend QA Playwright - version 1.1 - last updated: 2026-04-12 - by Laurie and Patrick

## Purpose

Use this skill to design, implement, review, and refine frontend automated tests with Playwright.

This skill is meant to support work such as:
- end-to-end testing of SPA frontend applications
- route and navigation validation
- authentication-aware user flow testing
- accessibility-conscious UI validation
- responsive behavior verification
- maintainable UI automation architecture
- regression protection for user-critical workflows
- page, layout, and component-level test abstraction

The expected outcome is stable, readable, maintainable Playwright test coverage that validates meaningful user behavior and supports long-term frontend quality.

---

## Engineering Principles

- prefer clarity over cleverness
- apply SRP (Single Responsibility Principle): tests, page objects, component objects, and utilities should have focused responsibilities
- apply DRY carefully: reduce wasteful duplication without creating harmful abstraction
- apply YAGNI: do not build speculative test layers or frameworks without present need
- prefer clean, readable, intention-revealing test code
- keep tests easy to understand, easy to debug, and easy to evolve
- choose maintainability and reliability over brittle test shortcuts
- let simplicity survive unless complexity is truly justified

---

## When to Use

Use this skill when:
- the frontend requires automated browser-based validation
- user-critical flows need regression coverage
- authentication, routing, forms, or UI workflows need end-to-end testing
- Playwright is the selected browser automation framework
- the project needs maintainable test architecture for pages, layouts, or shared components
- cross-browser or responsive validation is relevant
- accessibility-sensitive interaction patterns must be verified

Do not use this skill when:
- the work is purely backend
- the test need is better solved by unit or integration tests alone
- the task is purely product discovery without UI automation implications
- the project uses a different primary automation tool and Playwright is not part of the agreed stack

---

## Assumptions

Default assumptions for this skill:
- the frontend is tested with Playwright
- tests should align with documented feature behavior and project conventions
- test coverage should reflect feature risk and impact
- the repository is the source of truth for requirements, architecture, and testing intent
- test automation should support maintainability, not just short-term execution
- accessibility and responsive behavior matter where relevant
- Playwright should complement, not replace, lower-cost test layers
- browser-based end-to-end testing belongs near the top of the testing pyramid, not at its base

Unless explicitly stated otherwise:
- prefer stable selectors
- use Playwright for meaningful user-facing scenarios
- keep tests scenario-oriented and readable
- use the Page Object Model pattern for page-level interactions
- use Component Objects or Layout Objects for reusable UI structures and shared layouts
- avoid hiding business assertions inside page objects
- treat documentation updates as part of the work when test strategy or behavior changes

---

## Core Working Principles

- clarify the user flow or feature behavior before writing tests
- test meaningful behavior, not incidental implementation details
- keep tests scoped to the intended scenario
- prefer stable selectors and predictable interactions
- design for maintainability and debuggability
- treat flaky tests as quality problems, not normal inconvenience
- keep test architecture explicit and understandable
- update documentation when test strategy or expectations materially change
- surface tradeoffs clearly instead of hiding them in test abstraction
- do not push behavior into Playwright that should be covered more cheaply and clearly at lower test layers
---

## Recommended Workflow

1. Clarify the expected user behavior, scope, and risk
2. Identify which scenarios belong in unit, integration, or Playwright coverage
3. Identify impacted pages, layouts, components, and test objects
4. Design or update Page Objects, Component Objects, or Layout Objects as needed
5. Implement tests in scoped, readable steps
6. Refine selectors, assertions, and flow clarity
7. Validate reliability across relevant browsers, states, and screen sizes
8. Update related docs, ADRs, or standards when relevant

---

## Test Architecture Expectations

Prefer a maintainable Playwright architecture based on focused abstractions.

### Page Object Model
- prefer the Page Object Model pattern for page-level interactions
- each page object should represent a real user-facing page or major view
- page objects should expose meaningful interactions and stable UI access points
- page objects should not become giant dumping grounds for unrelated behavior

### Component Objects
- use Component Objects for reusable UI structures such as cards, modals, dialogs, form sections, tables, menus, and reusable widgets
- component objects should encapsulate repeated interactions and structure for shared UI parts
- keep component objects focused and reusable across tests when appropriate

### Layout Objects
- use Layout Objects for shared layout-level structures such as headers, footers, side navigation, top navigation, shell layouts, or persistent app chrome
- keep layout objects separate from page-specific behavior
- use layout objects when a shared layout contains real reusable UI behavior worth modeling

### Test Responsibilities
- keep tests scenario-oriented
- keep page, component, and layout objects focused on interaction and UI structure
- do not hide important business assertions deep inside test objects
- use test code to express the scenario and expected outcome clearly
- use test objects to reduce maintenance cost, not to create abstraction theater

---

## Selector Expectations

- prefer stable selectors over brittle CSS or text-only selectors
- use `data-testid`, `data-cy`, or other stable automation attributes where appropriate
- selectors should be intentional, durable, and readable
- avoid selectors tightly coupled to styling or visual structure
- avoid deep CSS chains that are likely to break from harmless UI refactors
- use semantic roles and accessible names when they are stable and meaningful
- add automation-friendly attributes deliberately when needed for reliability

---

## Scenario Design Expectations

- cover meaningful user journeys
- prioritize business-critical and regression-prone flows
- test happy paths and important non-happy paths
- validate unauthorized, forbidden, empty, loading, and error states where relevant
- verify route transitions and navigation flows deliberately
- test forms, submission behavior, and validation feedback where relevant
- keep each test focused enough to be diagnosable when it fails
- avoid writing one giant scenario that tries to validate the entire application at once
- each test should validate one coherent scenario intent, even if multiple related assertions are needed

---

## Authentication and Session Expectations

- explicitly validate auth-aware behavior where relevant
- verify protected route behavior
- verify unauthorized and forbidden states where relevant
- do not assume UI visibility alone proves real authorization correctness
- test login, logout, session expiration, and redirected flows when they are part of the product scope
- do not depend on insecure token storage assumptions
- keep session setup and teardown deliberate and understandable

---

## Accessibility and Responsive Testing Expectations

- include accessibility-sensitive interaction checks where relevant
- verify keyboard-reachable interactions for important flows
- ensure dialogs, menus, and forms remain usable through realistic navigation patterns
- verify that accessible labels, roles, and visible feedback work with the UI behavior being tested
- validate responsive behavior for flows where viewport differences matter
- use mobile-first thinking when selecting responsive scenarios
- do not treat accessibility and responsive testing as optional decoration on critical flows

---

## Network and Environment Expectations

- choose network mocking or real integration deliberately based on the test goal
- use mocks when isolating frontend behavior is the real objective
- use real backend integration when validating true cross-layer behavior is necessary
- avoid over-mocking until the test stops reflecting real user value
- avoid fully real integration when it makes tests slow, brittle, or hard to reason about without added value
- be explicit about environment assumptions
- keep test data and environment setup understandable and repeatable

---

## Playwright Standards

- keep Playwright usage explicit and understandable
- prefer readable locators and assertions
- use Playwright fixtures deliberately, not excessively
- keep helper utilities focused
- avoid building a second custom automation framework on top of Playwright unless justified
- keep retries, waits, and synchronization disciplined
- prefer deterministic waits over arbitrary sleeps
- avoid `waitForTimeout` except for rare debugging purposes
- make test setup, state preparation, and teardown visible and maintainable
- use traces, screenshots, and Playwright debugging tools deliberately when diagnosing instability or failures
- do not turn debugging artifacts into permanent noise without value

---

## Testing Expectations

### Testing Stack Preferences

Preferred defaults:
- Playwright
- stable automation attributes such as `data-testid` and `data-cy`
- CI-friendly execution and reporting
- browser coverage based on actual project needs

For test structure:
- always use `/* arrange */`, `/* act */`, `/* assert */`
- never use `/* given */`, `/* when */`, `/* then */`
- `given/when/then` is considered less clear in this context and too closely tied to Cucumber / BDD-style conventions
- test phases should remain immediately readable and explicit

Testing should reflect real risk, not just satisfy a ritual.

High test counts do not guarantee meaningful coverage.
A large test suite can still miss:
- edge cases
- failure paths
- auth/session issues
- accessibility regressions
- responsive regressions
- route transition problems
- business rule gaps
- regression-prone behaviors

Coverage is only one signal.
Tests should be designed to validate meaningful user behavior, including edge cases and non-happy-path scenarios.

### End-to-End Tests
Use for:
- authentication flows
- protected route behavior
- route transitions
- critical user journeys
- frontend/backend interaction through real interfaces where justified
- regression-prone business workflows

### Focused UI Workflow Tests
Use for:
- isolated but meaningful frontend scenarios
- form behavior
- component-heavy interaction flows
- modal, table, filter, and navigation interactions
- layout and shell behavior where reusable UI structure matters

### Cross-Viewport / Cross-Browser Validation
Use when relevant for:
- responsive flows
- browser-sensitive interactions
- critical user journeys with known compatibility risk

Also validate:
- invalid input
- unauthorized and forbidden access
- loading states
- empty states
- not found routes
- failure modes with meaningful UI behavior
- accessibility-sensitive interactions
- state restoration or transition behavior when relevant

---

## Documentation Expectations

Update documentation when relevant, including:
- feature docs when expected UI behavior changes
- testing strategy docs
- architecture docs when test architecture or object model patterns change
- ADRs when a meaningful testing or automation decision is made
- setup or CI notes when automation setup changes
- standards when new automation patterns are introduced

Do not let automated test intent drift away from documented product behavior without acknowledgment.

---

## Test Data Expectations

- test data should be predictable, isolated, and easy to understand
- avoid hidden dependence on mutable shared environments
- prefer deterministic setup over fragile cross-test coupling
- make seed, fixture, or setup assumptions explicit
- tests should not depend on accidental leftovers from previous runs
- test cases should never create test data that other tests depend on without explicit setup and teardown

---

## Test Pyramid Expectations

- Playwright sits near the top of the testing pyramid
- unit tests should cover isolated logic at the lowest and cheapest layer
- integration tests should cover component, boundary, or service interaction in the middle layer
- Playwright should cover high-value end-to-end behavior, not everything by default
- do not push low-level logic validation into expensive browser tests when cheaper layers can validate it more clearly
- use Playwright for critical journeys, auth flows, route transitions, integration-sensitive UI behavior, accessibility-sensitive interactions, and regression-prone flows where browser-level confidence is valuable

---

## What to Avoid

- brittle CSS-chain selectors
- over-reliance on text-only selectors when they are unstable
- giant page objects with mixed responsibilities
- hiding assertions deep inside page, layout, or component objects
- turning Playwright into an over-abstracted custom framework
- relying on arbitrary sleeps instead of deterministic synchronization
- writing end-to-end tests for behavior better covered by cheaper test layers
- skipping auth, error, loading, or edge-case scenarios on critical flows
- treating flaky tests as acceptable background noise
- using `/* given */`, `/* when */`, `/* then */` comments in tests
- assuming a large number of tests means the feature is meaningfully validated
- ignoring accessibility or responsive behavior on flows where they matter
- adding broad refactors inside a narrowly scoped testing task without explicit justification
- retrying flaky tests instead of understanding why they are flaky
- sharing state implicitly between tests
- depending on timing luck instead of deterministic readiness

---

## Definition of Done

A task using this skill is closer to done when:
- the tested user behavior is clearly validated
- test architecture remains understandable and maintainable
- page, layout, and component responsibilities remain clear
- stable selectors were used deliberately
- auth, error, and edge-case behavior were considered where relevant
- accessibility and responsive behavior were considered where relevant
- flaky behavior was reduced rather than normalized
- relevant documentation was updated
- known limitations or follow-ups were made explicit

---

## Example Tasks

- implement Playwright coverage for a protected SPA route and redirect behavior
- create Page Objects, Layout Objects, and Component Objects for a new feature area
- add regression coverage for a multi-step form flow with validation and error handling
- validate responsive navigation behavior across desktop and mobile layouts
- review whether a flaky Playwright test should be refactored, stabilized, or moved to another test layer
- add end-to-end coverage for login, logout, and unauthorized access behavior
- refactor an existing Playwright suite to improve readability, stability, and object responsibility boundaries

---

## Example Prompts

- "Implement Playwright coverage for this React feature using Page Objects, Component Objects, and stable selectors."
- "Review this Playwright test suite and identify architecture, flakiness, selector, and maintainability concerns."
- "Design a Playwright testing structure for this SPA flow, including Page Objects, shared layout objects, and critical path scenarios."
- "Refactor these Playwright tests to improve stability, readability, and responsibility separation without overengineering."