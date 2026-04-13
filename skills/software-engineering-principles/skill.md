# Software Engineering Principles - version 1.1 - last updated: 2026-04-12 - by Laurie and Patrick

## Purpose

Use this skill to guide software work with clear, durable, and practical engineering principles that apply across stacks, frameworks, and project types.

This skill is meant to support work such as:
- architecture and design decisions
- implementation quality
- refactoring discipline
- testing strategy
- documentation quality
- code review posture
- maintainability and readability improvements
- secure and production-conscious delivery

The expected outcome is software work that is easier to understand, easier to test, easier to evolve, and less likely to degrade into accidental complexity.

---

## Engineering Principles

- prefer clarity over cleverness
- apply SRP (Single Responsibility Principle): modules, classes, functions, and components should have focused responsibilities
- apply DRY carefully: reduce wasteful duplication without creating harmful or premature abstraction
- apply YAGNI: do not build speculative features, extension points, or abstractions without present need
- apply KISS: prefer the simplest solution that correctly solves the current problem
- prefer clean code that is readable, explicit, and intention-revealing
- keep code easy to understand, easy to test, and easy to evolve
- let simplicity survive unless complexity is truly justified
- make tradeoffs explicit instead of hiding them in implementation details
- treat secure coding, testing, and documentation as part of normal engineering work

---

## When to Use

Use this skill when:
- designing or reviewing software architecture
- implementing or refactoring features
- evaluating code quality
- deciding whether an abstraction is justified
- improving maintainability
- defining testing expectations
- reviewing whether documentation reflects implementation reality
- assessing whether code is production-conscious and sustainable

Do not use this skill when:
- the task requires stack-specific implementation guidance that belongs in a more specialized skill
- the work is purely non-technical
- the discussion is only about product desirability without engineering implications

---

## Assumptions

Default assumptions for this skill:
- the repository is the source of truth for architecture, standards, and delivery documentation
- secure coding is required by default
- test coverage should reflect feature risk and impact
- documentation should evolve with implementation
- maintainability matters even for fast-moving work
- readability is a feature, not a luxury

Unless explicitly stated otherwise:
- prefer explicit and understandable code
- prefer scoped changes over opportunistic sprawl
- avoid silent architecture drift
- treat technical debt consciously rather than accidentally
- consider future maintainers part of the audience of the code

---

## Core Working Principles

- clarify the problem before designing the solution
- solve the real problem, not an imagined future variation of it
- choose abstractions only when they reduce real complexity
- keep responsibilities visible
- make important decisions and tradeoffs explicit
- optimize for maintainability and clarity first
- avoid coupling unrelated concerns
- use tests to validate behavior, not just to inflate numbers
- use documentation to preserve project memory
- challenge weak assumptions before they harden into structure

---

## Recommended Workflow

1. Clarify the objective, scope, and constraints
2. Identify the simplest viable approach
3. Check whether the design respects responsibility boundaries
4. Evaluate whether duplication is harmful or still acceptable at the current stage
5. Avoid speculative abstraction unless a real need exists
6. Implement in clear, scoped steps
7. Review naming, structure, and maintainability
8. Validate with meaningful tests
9. Update documentation when the project truth changed
10. Make limitations, risks, and follow-ups explicit

---

## Design and Maintainability Expectations

- each module should have a clear reason to exist
- each class, component, or service should have focused responsibilities
- each function should do one coherent thing
- boundaries between concerns should remain visible
- abstraction should reduce complexity, not relocate it
- duplication should be evaluated carefully: not all duplication is equally harmful
- premature deduplication can be worse than temporary duplication
- naming should communicate intent clearly
- code should be readable without requiring private tribal knowledge
- design should remain open to evolution without becoming speculative or bloated

---

## Clean Code Expectations

- prefer intention-revealing names
- prefer explicit behavior over hidden magic
- keep code paths understandable
- avoid giant units that mix multiple responsibilities
- avoid opaque cleverness that saves lines but increases cognitive load
- write code that another competent developer can follow without reverse-engineering your thought process
- favor readability, coherence, and local understandability
- comments should clarify intent, tradeoff, or non-obvious context, not compensate for avoidable code confusion

---

## Abstraction Expectations

- create abstractions when they reduce repeated complexity or clarify intent
- do not create abstractions just because duplication exists once or twice
- do not build extension points for imaginary future requirements
- avoid abstraction layers that hide simple flows behind unnecessary indirection
- prefer concrete and understandable code until a real pattern proves the need for extraction
- revisit abstractions when requirements actually evolve

---

## Secure Coding Expectations

- treat security as standard engineering discipline, not as a late-stage add-on
- validate external input
- respect trust boundaries
- enforce authentication and authorization where relevant
- avoid exposing sensitive data carelessly
- avoid insecure defaults for the sake of speed
- document meaningful security assumptions and risks
- surface uncertainty instead of pretending risk has been solved

---

## Testing Expectations

Testing should validate meaningful behavior, not merely satisfy a coverage target.

- use tests to confirm behavior, edge cases, and failure paths
- keep test structure explicit and easy to scan
- always use `/* arrange */`, `/* act */`, `/* assert */`
- never use `/* given */`, `/* when */`, `/* then */`
- coverage is only one signal, not proof of correctness
- 100% code coverage does not mean a feature is fully tested
- edge cases must be considered explicitly
- non-happy-path scenarios matter
- authorization, validation, and error flows matter
- tests should reflect actual risk, not ritual compliance

---

## Documentation Expectations

- documentation should reflect reality closely enough to be trusted
- architecture decisions should be recorded when they matter
- feature behavior should not drift silently away from docs
- standards should be updated when the project introduces new patterns
- documentation should preserve why something was built, not just what exists now
- the repository should remain the project’s durable memory

---

## Code Review Expectations

- review for clarity, not just correctness
- review responsibility boundaries
- review whether abstraction is justified
- review naming quality
- review whether the implementation introduced hidden coupling
- review security-sensitive behavior
- review whether tests are meaningful
- review whether edge cases and failure paths were considered
- review whether docs should be updated
- challenge ambiguity respectfully and explicitly

---

## What to Avoid

- clever code that obscures intent
- premature abstraction
- speculative extensibility
- giant modules with mixed responsibilities
- deduplicating too early and creating worse indirection
- hidden tradeoffs
- silent architecture drift
- pretending high coverage means sufficient testing
- ignoring edge cases
- using `/* given */`, `/* when */`, `/* then */` in tests
- undocumented decisions that materially affect the project
- treating documentation as decoration
- treating security as optional until later

---

## Definition of Done

A task using this skill is closer to done when:
- the real problem is addressed
- the chosen solution remains understandable
- responsibilities are clear
- abstraction is justified
- maintainability was preserved or improved
- security-sensitive aspects were considered
- tests are meaningful, not merely numerous
- edge cases and failure paths were considered
- relevant documentation was updated
- known tradeoffs, limitations, or follow-ups were made explicit

---

## Example Tasks

- review whether a proposed abstraction is justified or premature
- refactor a service or component to better respect SRP
- evaluate whether duplication should be removed or tolerated for now
- review a feature for maintainability, testability, and clarity
- improve naming and structure in a codebase that has become hard to navigate
- assess whether documentation and implementation still match
- identify where a design is violating YAGNI or introducing unnecessary complexity

---

## Example Prompts

- "Review this implementation and identify violations of SRP, DRY, YAGNI, KISS, and clean code principles."
- "Help me decide whether this abstraction is justified or premature."
- "Refactor this code to improve readability, responsibility boundaries, and maintainability without overengineering it."
- "Evaluate whether this feature is meaningfully tested or only superficially covered."