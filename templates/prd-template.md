# PRD: <product-or-feature-title> - last updated: 2024-06-17 - by Laurie and Patrick

- Status: Draft / Proposed / Approved / Superseded
- Date: YYYY-MM-DD
- Owners:
- Related BRD:
- Related ARD:
- Related ADR(s):
- Related Feature(s):

---

## Executive Summary

Provide a concise summary of the product or feature.

Answer:
- what is being built
- who it is for
- what problem it solves
- why it matters now
- what outcome is expected

Keep this section easy to understand for both product and technical stakeholders.

---

## Background and Context

Describe the context behind this product or feature.

Include:
- current situation
- user or business problem
- existing limitations or pain points
- why this initiative exists now
- any relevant business, technical, or operational context

---

## Problem Statement

Clearly state the problem this PRD addresses.

Examples:
- Users cannot ...
- Administrators have no way to ...
- The current process causes ...
- The existing solution does not support ...

---

## Goals

List the intended goals.

Examples:
- enable users to ...
- reduce ...
- improve ...
- support ...
- make ... possible

Goals should be outcome-oriented, not implementation-oriented.

---

## Non-Goals

Document what this PRD does not attempt to solve right now.

Examples:
- mobile support
- advanced analytics
- multi-tenant behavior
- full workflow automation
- role administration UI

This helps prevent scope drift.

---

## Scope

In scope:
- ...
- ...
- ...

Out of scope:
- ...
- ...
- ...

---

## Target Users / Actors

Identify who will interact with the product or feature.

Examples:
- anonymous users
- authenticated users
- administrators
- support staff
- internal operators
- external partners
- system integrations

For each actor, briefly note what they need from the feature.

---

## User Stories / Use Cases

Examples:
- As a user, I want to ..., so that ...
- As an administrator, I want to ..., so that ...
- As a support agent, I want to ..., so that ...

List the key use cases that define the expected behavior.

---

## Functional Requirements

List the required functional behavior.

### FR-001
Description:
- ...

Acceptance notes:
- ...

### FR-002
Description:
- ...

Acceptance notes:
- ...

### FR-003
Description:
- ...

Acceptance notes:
- ...

Repeat as needed.

---

## Non-Functional Requirements

Document the quality expectations that matter.

Examples:
- performance expectations
- reliability expectations
- accessibility requirements
- observability requirements
- localization requirements
- maintainability expectations
- compliance constraints
- data retention expectations

### NFR-001
Description:
- ...

### NFR-002
Description:
- ...

Repeat as needed.

---

## User Experience Notes

Document any experience or interface expectations.

Examples:
- empty states must be explicit
- errors must be understandable
- the flow should minimize friction
- forms should validate clearly
- loading states should be visible
- success states should confirm the outcome

If UX details are not yet decided, say so.

---

## Security and Privacy Requirements

Document the security and privacy expectations for this product or feature.

Examples:
- authentication required
- authorization rules
- sensitive data handling
- auditability expectations
- rate limiting or abuse protection
- logging restrictions
- session or token constraints
- retention or deletion expectations

Do not leave this section implicit for risky features.

---

## Assumptions

Document important assumptions.

Examples:
- users already have accounts
- the backend API already exists
- the data model can be extended safely
- internal admins are authenticated through the standard auth flow

If an assumption is risky, note it.

---

## Constraints

Document important constraints.

Examples:
- existing stack must be preserved
- timeline is limited
- only certain roles can access the feature
- the solution must fit into an existing architecture
- the deployment model is fixed
- the feature must be backward compatible

---

## Dependencies

List dependencies that affect delivery.

Examples:
- another feature
- backend endpoint availability
- design assets
- infrastructure setup
- auth readiness
- third-party integration
- migration work

---

## Edge Cases and Failure Modes

Document important edge cases.

Examples:
- empty state
- missing data
- invalid input
- duplicate submission
- partial failure
- timeout
- unauthorized access
- rate-limited user
- stale data
- not found condition

---

## Acceptance Criteria

List the feature-level acceptance criteria clearly.

- ...
- ...
- ...
- ...

Acceptance criteria should be specific and testable.

---

## Success Measures

Document how success will be evaluated.

Examples:
- reduced manual effort
- improved completion rate
- lower support burden
- reduced failure rate
- faster task completion
- fewer incidents in a specific flow

Use qualitative or quantitative measures as appropriate.

---

## Architecture Impact

Summarize the expected architecture impact.

Examples:
- new API endpoints
- new UI components
- service changes
- database changes
- auth changes
- background processing
- documentation updates

Reference detailed architecture docs where needed.

---

## Testing Expectations

Describe how this PRD should be validated.

Examples:
- core business rules covered by unit tests
- service and persistence interactions covered by integration tests
- critical user journeys covered by end-to-end tests
- manual validation needed for UX flows
- security-sensitive paths explicitly tested

---

## Rollout / Delivery Notes

Document how this work is expected to be delivered.

Examples:
- single release
- phased rollout
- behind feature flag
- admin-only first
- internal validation before public release

If not yet decided, say so.

---

## Documentation Impact

List documentation that must be created or updated:
- BRD
- ARD
- ADRs
- feature docs
- standards
- API docs
- setup or operational notes

---

## Open Questions

List unresolved questions:
- ...
- ...
- ...

---

## Risks

List product or delivery risks:
- ...
- ...
- ...

Include mitigation or follow-up where useful.

---

## Revision Notes

Track major changes to this PRD.

- YYYY-MM-DD: Initial draft
- YYYY-MM-DD: Updated scope
- YYYY-MM-DD: Revised after architecture review
