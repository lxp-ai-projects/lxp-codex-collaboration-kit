# Secure Coding - version 1.0 - last updated: 2026-04-12 - by Laurie and Patrick

## Purpose

Use this skill to design, implement, review, and refine software with secure coding practices as a normal part of engineering work.

This skill is meant to support work such as:
- secure API and application design
- input validation and trust-boundary handling
- authentication and authorization flows
- sensitive data handling
- secure configuration and secret management
- defensive coding and error handling
- security-aware code review
- security-conscious testing and delivery

The expected outcome is software that is more resilient, less exposed to common security mistakes, and built with security as a deliberate engineering concern rather than a last-minute add-on.

---

## Engineering Principles

- treat security as standard engineering discipline, not as a final checklist item
- prefer secure defaults over convenience shortcuts
- validate assumptions at trust boundaries
- make security-sensitive behavior explicit
- apply least privilege where relevant
- prefer clarity over cleverness in security-critical code
- keep secure behavior understandable, testable, and reviewable
- surface uncertainty instead of pretending risk has already been addressed
- let security controls remain visible rather than hidden behind accidental complexity

---

## When to Use

Use this skill when:
- designing or reviewing application behavior that crosses trust boundaries
- implementing authentication, authorization, token, cookie, or session flows
- handling user input, file uploads, external payloads, or third-party integrations
- storing, transmitting, or displaying sensitive data
- reviewing API behavior for abuse, injection, or access control risks
- designing secure defaults for frontend or backend systems
- evaluating whether implementation choices introduce avoidable attack surface

Do not use this skill when:
- the task is purely non-technical
- the work is entirely unrelated to application behavior, data handling, or system interaction
- a more specialized security or infrastructure skill is required for a deeper domain-specific concern

---

## Assumptions

Default assumptions for this skill:
- secure coding is required by default
- the repository is the source of truth for architecture, standards, and delivery documentation
- input and external state must not be trusted blindly
- security-sensitive decisions should be documented when they materially affect the architecture
- tests should reflect security-sensitive risk, not just happy-path behavior
- security and maintainability should reinforce each other, not compete unnecessarily

Unless explicitly stated otherwise:
- validate external input
- do not trust client-side restrictions as sufficient protection
- do not expose sensitive internal details carelessly
- avoid insecure defaults for the sake of speed
- treat secrets, tokens, cookies, and configuration as high-sensitivity areas
- document meaningful security assumptions, constraints, and tradeoffs

---

## Core Working Principles

- identify trust boundaries before implementing features
- validate input at system boundaries
- separate authentication from authorization
- fail safely and explicitly
- keep security controls understandable
- do not rely on obscurity as a control
- make data sensitivity visible in design and implementation
- challenge assumptions that reduce security posture for convenience
- review security impact when adding new endpoints, flows, storage, or integrations
- keep documentation aligned with security-relevant behavior

---

## Recommended Workflow

1. Clarify the feature, data flow, and trust boundaries
2. Identify sensitive inputs, outputs, and state transitions
3. Identify authentication, authorization, and validation expectations
4. Evaluate secure defaults, error handling, and data exposure risks
5. Implement in clear, scoped steps
6. Review logs, secrets, tokens, cookies, and sensitive outputs
7. Add or update tests for security-sensitive paths and failure cases
8. Update related docs, ADRs, or standards when relevant

---

## Threat and Risk Awareness

- identify who can call or reach the feature
- identify what data is sensitive, user-controlled, privileged, or externally sourced
- identify what assumptions are being made about identity, role, origin, or payload validity
- identify where the system can be abused, not just how it works when used correctly
- think in terms of misuse, not only intended use
- evaluate how a failure would behave under malicious, unexpected, or repeated input
- document meaningful tradeoffs when risk is knowingly accepted

---

## Input Validation Expectations

- validate all external input
- prefer allowlists and explicit constraints over vague acceptance
- treat request bodies, query params, headers, cookies, uploaded files, and external payloads as untrusted
- do not rely on frontend validation alone
- reject malformed, unexpected, or unauthorized input early
- keep validation rules explicit and understandable
- avoid silently coercing dangerous or ambiguous values
- ensure validation failures are safe, consistent, and non-leaky

---

## Authentication and Authorization Expectations

- treat authentication and authorization as separate concerns
- verify identity explicitly where required
- verify permission explicitly where required
- apply least privilege
- do not assume that hidden UI elements enforce access control
- do not assume route guards or middleware alone replace proper downstream checks when deeper control is needed
- make role or permission expectations visible in implementation and docs
- handle unauthorized and forbidden cases deliberately
- review token, session, cookie, and refresh behavior carefully when they are part of the feature

---

## Secrets and Configuration Expectations

- never hardcode secrets
- use environment variables or secure secret management mechanisms
- do not expose secrets in logs, examples, screenshots, or commits
- keep security-relevant configuration explicit and understandable
- avoid insecure fallback defaults for production-sensitive settings
- document required runtime configuration when relevant
- review secret usage in local development, CI, containers, and deployment paths

---

## Data Protection Expectations

- minimize collection and exposure of sensitive data
- avoid returning internal implementation details in user-facing errors
- avoid logging sensitive payloads carelessly
- protect tokens, credentials, personal data, and internal identifiers appropriately
- be explicit about which system is the source of truth for sensitive state
- respect retention, deletion, and exposure constraints when relevant
- treat cached or replicated sensitive data as still sensitive

---

## Frontend Security Expectations

- do not store JWT auth tokens in local storage by default
- prefer secure cookie-based auth flows with HttpOnly cookies when appropriate
- do not treat client-side checks as real authorization
- avoid exposing sensitive state or internal details in the UI
- be careful with browser storage, logs, and debug output
- validate assumptions about CORS, CSRF, XSS, and trusted origins where relevant
- ensure user-facing error handling does not leak internal details
- keep security-sensitive UI behavior aligned with backend truth

---

## Backend Security Expectations

- validate input at API boundaries
- enforce authentication and authorization explicitly
- avoid leaking stack traces or internal implementation details in public responses
- review broken access control risk whenever adding or modifying an endpoint
- review injection risk in persistence, queries, templates, or dynamic behavior
- fail safely when validation or authorization fails
- keep security-sensitive flows explicit and reviewable
- document security-relevant operational assumptions when they materially affect behavior

---

## API Security Expectations

- keep contracts explicit
- validate request shapes and boundary assumptions
- document authorization expectations clearly
- avoid overexposing internal fields in responses
- design errors intentionally
- enforce idempotency, rate protection, or abuse controls when relevant
- consider replay, brute-force, enumeration, and flooding risks where applicable
- do not assume an endpoint is safe just because it works correctly under normal use

---

## Logging and Observability Expectations

- log enough to support diagnosis and incident understanding
- do not log secrets, credentials, tokens, or sensitive payloads carelessly
- keep security-relevant failures observable
- distinguish internal diagnostic detail from public-facing error detail
- ensure alerts, logs, or traces do not become their own leakage vector
- make security-relevant operational assumptions visible when they matter

---

## Dependency and Supply Chain Expectations

- prefer maintained, reputable dependencies
- avoid unnecessary dependencies
- do not add libraries casually to solve tiny problems
- review whether a dependency meaningfully expands attack surface
- be cautious with copied code, snippets, or packages from untrusted sources
- keep dependency choices understandable and justifiable
- update or replace problematic dependencies deliberately when risk is known

---

## Secure Coding Review Expectations

- review trust boundaries
- review validation completeness
- review authentication and authorization expectations
- review sensitive data exposure
- review logs and error messages
- review cookie, token, or session handling
- review dangerous defaults
- review abuse and misuse paths
- review whether the implementation is secure only in the happy path or also under hostile or invalid behavior
- challenge weak assumptions respectfully and explicitly

---

## Testing Expectations

Testing should validate security-sensitive behavior, not merely happy-path correctness.

- test invalid input
- test unauthorized and forbidden access
- test failure paths
- test abuse-sensitive boundaries where relevant
- test token, cookie, session, or auth lifecycle behavior where relevant
- test validation and authorization together when flows depend on both
- coverage is only one signal, not proof of security
- 100% code coverage does not mean security-relevant behavior is sufficiently tested
- edge cases, malformed input, and non-happy-path behavior matter
- security-sensitive paths deserve explicit review and validation

For test structure:
- always use `/* arrange */`, `/* act */`, `/* assert */`
- never use `/* given */`, `/* when */`, `/* then */`

---

## Documentation Expectations

Update documentation when relevant, including:
- feature docs when security-relevant behavior changes
- architecture docs when trust boundaries, token flows, or data protection assumptions change
- ADRs when meaningful security decisions are made
- standards when new security patterns are introduced
- setup or operational notes when security-relevant configuration changes
- testing notes when new security-sensitive validation paths are added

Do not let security-relevant behavior drift away from documented project truth without acknowledgment.

---

## What to Avoid

- trusting client input by default
- treating authentication as sufficient without authorization
- hardcoding secrets
- logging sensitive data carelessly
- storing JWT auth tokens in local storage by default
- exposing stack traces or internal details in public errors
- assuming hidden UI equals access control
- assuming happy-path behavior proves secure behavior
- weakening security controls for convenience without explicit tradeoff discussion
- relying on obscure behavior instead of explicit controls
- pretending high coverage means security is adequately tested
- ignoring malformed input, hostile use, or abuse paths
- treating security review as optional until later

---

## Definition of Done

A task using this skill is closer to done when:
- trust boundaries were identified
- security-sensitive behavior is explicit and understandable
- input validation is deliberate
- authentication and authorization expectations were handled correctly
- secrets, tokens, cookies, and sensitive data were treated appropriately
- relevant failure paths and misuse paths were considered
- security-sensitive tests were added or updated where appropriate
- relevant documentation was updated
- known tradeoffs, limitations, or follow-ups were made explicit

---

## Example Tasks

- review an auth flow for token, cookie, and authorization risks
- evaluate whether a frontend implementation exposes sensitive auth data unsafely
- harden an API endpoint against validation and access-control mistakes
- review logging behavior for sensitive data leakage
- assess whether a feature handles malformed input safely
- design secure defaults for a new user-facing or admin-facing flow
- identify whether Redis, cookies, tokens, or caches are being used in a way that creates security ambiguity

---

## Example Prompts

- "Review this implementation for input validation, auth/authz, token handling, logging hygiene, and sensitive data exposure risks."
- "Help me harden this feature against common secure coding mistakes without overengineering it."
- "Evaluate whether this frontend/backend flow treats cookies, tokens, and trust boundaries safely."
- "Identify which security assumptions in this feature should be documented explicitly."