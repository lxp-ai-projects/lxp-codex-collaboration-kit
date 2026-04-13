# GitHub Action CI - version 1.0 - last updated: 2026-04-12 - by Laurie and Patrick

## Purpose

Use this skill to design, implement, review, and refine CI workflows with GitHub Actions.

This skill is meant to support work such as:
- continuous integration workflow design
- pull request validation
- build and test automation
- linting and formatting enforcement
- contract and documentation validation
- artifact generation
- reusable workflow design
- secure CI configuration
- maintainable automation for multi-stack repositories

The expected outcome is CI automation that is clear, reliable, secure, maintainable, and aligned with project architecture, delivery standards, and repository conventions.

---

## Engineering Principles

- prefer clarity over cleverness
- keep workflows easy to understand, debug, and evolve
- apply SRP (Single Responsibility Principle): each workflow, job, and reusable action should have a focused purpose
- apply DRY carefully: reduce wasteful duplication without hiding intent behind excessive indirection
- apply YAGNI: do not build speculative workflow complexity without present need
- prefer explicit and maintainable CI behavior over fragile optimization tricks
- keep security controls visible and understandable
- let simplicity survive unless complexity is truly justified

---

## When to Use

Use this skill when:
- setting up or improving CI in a GitHub repository
- validating pull requests and protected branches
- automating linting, formatting, builds, tests, and quality gates
- supporting backend, frontend, or multi-stack repositories with GitHub Actions
- designing reusable workflows across projects or modules
- enforcing repository standards through automation
- reviewing whether CI is maintainable, secure, and aligned with project delivery needs

Do not use this skill when:
- the task is unrelated to repository automation
- another CI platform is the agreed standard and GitHub Actions is not part of the workflow
- the work is purely product discovery with no automation implications

---

## Assumptions

Default assumptions for this skill:
- the repository uses GitHub as the source of truth for code and collaboration
- CI should run on pull requests and/or protected branches where appropriate
- secure coding is required by default
- CI must reflect real project quality expectations, not just superficial pass/fail checks
- workflow design should remain traceable to project needs
- the repository is the source of truth for standards, architecture, and delivery documentation

Unless explicitly stated otherwise:
- prefer GitHub Actions for CI workflow automation
- keep workflows explicit and readable
- prefer incremental and composable jobs over giant all-in-one pipelines
- enforce meaningful quality gates
- treat secrets and tokens as sensitive
- prefer reproducibility over “works on my runner” assumptions
- document CI assumptions when they materially affect delivery

---

## Core Working Principles

- clarify the pipeline objective before writing YAML
- automate meaningful checks, not vanity checks
- align CI with the project’s actual stack and standards
- keep jobs focused and diagnosable
- fail fast where it improves feedback quality
- make quality gates explicit
- keep CI secure by default
- prefer maintainable workflow structure over clever YAML gymnastics
- update documentation when automation behavior materially changes
- surface tradeoffs clearly instead of hiding them in the pipeline

---

## Recommended Workflow

1. Clarify the repository structure, stack, and CI goals
2. Identify what should run on push, pull request, release, or manual dispatch
3. Separate fast feedback checks from heavier validation where appropriate
4. Design workflow, jobs, and reusable steps explicitly
5. Implement with clear triggers, conditions, and naming
6. Review cache, concurrency, artifact, and secret handling
7. Validate reliability, speed, and diagnosability
8. Update related docs, ADRs, or standards when relevant

---

## Workflow Design Expectations

- keep workflows focused on a clear responsibility
- prefer multiple clear workflows over one giant workflow when separation improves maintainability
- keep workflow names, job names, and step names readable
- use explicit triggers and conditions
- avoid hidden coupling between unrelated jobs
- make failure reasons easy to understand from the workflow output
- ensure PR workflows reflect actual merge quality expectations
- separate CI concerns from deployment concerns unless the project intentionally combines them

---

## Job and Step Design Expectations

- keep jobs cohesive and diagnosable
- prefer meaningful step names
- keep shell scripts understandable
- avoid large opaque inline scripts when maintainability suffers
- use reusable workflows or composite actions when duplication becomes real and repeated
- avoid abstraction for its own sake
- ensure job dependencies are explicit
- design jobs so failures are understandable without reverse-engineering the entire workflow

---

## Trigger and Branch Expectations

- define triggers deliberately
- use pull request validation for branch protection where appropriate
- use push triggers for relevant branch-level verification
- use workflow_dispatch when manual execution is useful
- avoid triggering expensive workflows unnecessarily
- align branch targeting with project delivery conventions
- make path filters explicit when monorepo or multi-module repositories benefit from them

---

## Caching and Performance Expectations

- use caching deliberately when it improves CI efficiency without compromising reliability
- cache dependency layers and build artifacts only when the cache strategy is understandable
- do not let cache assumptions hide broken reproducibility
- prefer predictable pipelines over marginal speed gains from fragile caching
- review cache invalidation behavior explicitly
- optimize the feedback loop, but not at the cost of trustworthiness

---

## Matrix and Multi-Stack Expectations

- use matrix builds when they add real value
- avoid matrix complexity when a single environment is sufficient
- keep matrix dimensions explicit and meaningful
- support multi-stack repositories deliberately
- ensure backend, frontend, contract, and QA checks remain understandable when combined
- do not overload a single workflow with unrelated matrix permutations without clear benefit

---

## Quality Gate Expectations

- CI should enforce meaningful quality gates
- validate linting, formatting, build health, and relevant test layers
- enforce stack-specific validation where appropriate
- validate OpenAPI or contract artifacts when the project is contract-first
- validate documentation or generated artifacts when they are part of the expected workflow
- do not treat green CI as proof of total quality
- use CI to reinforce standards, not replace engineering judgment

---

## Secure CI Expectations

- treat secrets, tokens, and credentials as high-sensitivity inputs
- use GitHub secrets or approved secure secret sources
- do not hardcode secrets in workflows
- minimize token permissions
- prefer least privilege for workflow permissions
- avoid exposing secrets through logs, artifacts, or debug output
- be explicit about which jobs need elevated access
- review third-party actions before adopting them
- pin actions deliberately when the project requires stronger supply-chain control
- do not assume CI is safe just because it runs in GitHub-hosted infrastructure

---

## Artifact and Output Expectations

- publish artifacts only when they serve a real workflow purpose
- keep artifact naming and retention understandable
- do not retain unnecessary sensitive outputs
- distinguish temporary debugging artifacts from meaningful deliverables
- make generated reports, test outputs, or build artifacts easy to interpret when relevant
- keep artifacts aligned with actual delivery and review needs

---

## Reusable Workflow Expectations

- use reusable workflows when duplication is real across repositories or workflow files
- keep reusable workflow interfaces explicit and stable
- do not create abstraction layers that hide simple workflow behavior
- document required inputs, secrets, and expected outputs
- prefer reuse that improves consistency without harming readability
- review whether reuse is justified before extracting

---

## Stack-Aware Expectations

When relevant, CI should align with the repository stack.

Examples:
- Kotlin / Spring Boot: build, lint, unit tests, integration tests, contract validation, container checks when relevant
- React / Vite: lint, format, type-check, unit tests, build, Playwright or UI automation when relevant
- NestJS: lint, type-check, unit tests, integration tests, contract checks when relevant
- OpenAPI-first repositories: validate spec integrity and contract alignment
- Docker-based repositories: validate compose or image build behavior when relevant

Do not run stack-inappropriate checks mechanically just for symmetry.

---

## Testing Expectations

Testing inside CI should validate meaningful project behavior, not just exercise commands.

- use CI to run the right test layers for the repository
- separate fast feedback from heavier validation where appropriate
- ensure failures remain diagnosable
- do not overload every PR with slow end-to-end suites unless the project truly requires it
- coverage is only one signal, not proof of sufficient testing
- 100% coverage does not mean a feature is fully tested
- edge cases and non-happy-path behavior still matter
- CI should reinforce the project’s testing strategy, not distort it

For test structure and standards:
- align with repository testing conventions
- where code examples are involved, prefer `/* arrange */`, `/* act */`, `/* assert */`
- never use `/* given */`, `/* when */`, `/* then */` as a default testing convention

---

## Documentation Expectations

Update documentation when relevant, including:
- CI setup notes
- contributor guides
- repository standards
- ADRs when meaningful pipeline or automation decisions are made
- quality gate expectations
- artifact or workflow usage notes
- setup instructions when local and CI behavior must align

Do not let repository expectations drift away from CI reality without acknowledgment.

---

## What to Avoid

- giant workflows with unclear responsibilities
- opaque step names
- hidden coupling between unrelated jobs
- hardcoded secrets
- excessive permissions by default
- adding third-party actions casually without review
- overusing caching without understanding invalidation
- running every expensive check on every event without reason
- abstracting workflows so much that nobody can debug them
- treating green CI as proof that the system is fully validated
- assuming high coverage means the feature is fully tested
- ignoring edge cases because the pipeline passes
- mixing deployment logic into CI accidentally
- letting workflow behavior drift away from documented project standards

---

## Definition of Done

A task using this skill is closer to done when:
- the CI objective is clear
- workflow, job, and step responsibilities are understandable
- triggers and branch behavior are deliberate
- quality gates reflect actual project needs
- security-sensitive aspects of CI were considered
- caching, artifacts, and reuse are justified and understandable
- failures remain diagnosable
- relevant documentation was updated
- known tradeoffs, limitations, or follow-ups were made explicit

---

## Example Tasks

- create a PR validation workflow for a Kotlin Spring Boot backend
- create a CI workflow for a React Vite frontend with lint, format, type-check, unit tests, and build
- add contract validation for an OpenAPI-first repository
- split an oversized CI workflow into clearer responsibilities
- review whether a workflow is over-permissioned or leaks sensitive data
- add matrix validation for a multi-module or multi-environment repository
- create reusable workflows for shared quality gates across repositories

---

## Example Prompts

- "Design a GitHub Actions CI workflow for this repository, including appropriate triggers, quality gates, and security-conscious defaults."
- "Review this GitHub Actions workflow for readability, maintainability, caching strategy, and secret handling concerns."
- "Help me split this oversized CI workflow into clearer jobs or reusable workflows."
- "Design CI quality gates for this stack so pull requests get fast but meaningful feedback."