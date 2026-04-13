# Docker Compose Developer - version 1.0 - last updated: 2026-04-12 - by Laurie and Patrick

## Purpose

Use this skill to design, implement, review, and refine Docker Compose configurations for local development, lightweight multi-service orchestration, and delivery-supporting environments.

This skill is meant to support work such as:
- local development environments
- backend, frontend, database, and cache orchestration
- service dependency wiring
- environment configuration for development or validation
- developer experience improvements
- reproducible local startup
- lightweight integration environments
- maintainable container composition

The expected outcome is a Docker Compose setup that is clear, reliable, secure enough for its intended scope, easy to understand, and aligned with project architecture and development workflow.

---

## Engineering Principles

- prefer clarity over cleverness
- keep compose files easy to understand, debug, and evolve
- apply SRP (Single Responsibility Principle): each service should have a clear purpose
- apply DRY carefully: reduce wasteful duplication without hiding intent behind excessive indirection
- apply YAGNI: do not add orchestration complexity without present need
- prefer explicit and maintainable service definitions
- keep environment assumptions visible
- let simplicity survive unless complexity is truly justified

---

## When to Use

Use this skill when:
- defining or improving local multi-service development environments
- orchestrating backend, frontend, database, cache, queue, or supporting services locally
- creating a reproducible developer environment
- supporting integration-style local validation
- standardizing service startup and dependency wiring
- making a project easier to run consistently across machines
- validating containerized behavior without introducing heavier orchestration

Do not use this skill when:
- the task requires full production orchestration that belongs to Kubernetes, Nomad, or another platform
- the work is unrelated to containerized service composition
- Docker Compose is not part of the agreed local or delivery workflow
- the task is purely product discovery with no runtime or environment implications

---

## Assumptions

Default assumptions for this skill:
- Docker Compose is used for local development, lightweight orchestration, or validation environments
- the repository is the source of truth for setup, architecture, and delivery documentation
- secure coding is required by default
- service definitions should remain understandable and traceable to real project needs
- environment setup should support maintainability and developer productivity
- containerized local behavior should remain reproducible across machines

Unless explicitly stated otherwise:
- keep service names explicit and meaningful
- keep ports, volumes, environment variables, and dependencies readable
- prefer explicit composition over fragile hidden behavior
- treat secrets and sensitive configuration carefully even in local setups
- document assumptions when compose behavior materially affects development or validation workflow

---

## Core Working Principles

- clarify the purpose of the compose setup before writing it
- compose only the services that add real value to the intended environment
- keep service responsibilities explicit
- prefer reproducible local startup over ad hoc machine-specific setup
- keep environment assumptions visible
- keep dependency wiring understandable
- do not treat compose as a dumping ground for unrelated runtime behavior
- update documentation when environment behavior materially changes
- surface tradeoffs clearly instead of hiding them in YAML

---

## Recommended Workflow

1. Clarify the environment goal, scope, and intended users
2. Identify which services must run together and why
3. Define service boundaries, ports, volumes, networks, and environment variables
4. Add healthchecks, startup dependencies, and persistence only where they add real value
5. Review developer experience, reproducibility, and diagnosability
6. Validate startup, shutdown, and cross-service interaction behavior
7. Refine naming, structure, and environment assumptions
8. Update related docs, ADRs, or standards when relevant

---

## Compose Design Expectations

- keep compose files focused on a clear environment purpose
- prefer readable service definitions over compact but opaque YAML
- use meaningful service names
- separate concerns cleanly between services
- keep dependencies understandable
- avoid stuffing too many unrelated concerns into one compose setup
- use multiple compose files or overrides only when they improve maintainability
- prefer a structure that another developer can understand quickly without tribal knowledge

---

## Service Definition Expectations

- each service should have a clear role
- define images or builds explicitly
- define ports deliberately
- define volumes deliberately
- define environment variables clearly
- avoid overloading services with hidden startup logic
- keep command and entrypoint overrides understandable
- ensure service behavior remains diagnosable when startup fails
- avoid burying important behavior in overly complex shell wrappers unless justified

---

## Networking Expectations

- use networks deliberately
- keep service communication understandable
- expose only what is needed to the host machine
- avoid unnecessary port exposure
- prefer container-to-container communication over host-based assumptions when appropriate
- make network naming and purpose understandable
- do not create unnecessary network complexity without real value

---

## Volume and Data Expectations

- use volumes deliberately
- distinguish persistent data from ephemeral data
- keep bind mounts and named volumes understandable
- avoid accidental data loss through careless volume design
- avoid unnecessary persistence for disposable services
- document when local persistence materially affects development workflow
- ensure developers can understand what data survives restarts and what does not

---

## Environment and Configuration Expectations

- keep environment variables explicit and understandable
- use `.env` or other approved configuration approaches deliberately
- do not hardcode secrets in compose files
- distinguish required configuration from optional configuration
- make service-level configuration predictable
- avoid fragile machine-specific assumptions in paths, ports, or environment values
- document important runtime assumptions when relevant

---

## Dependency and Startup Expectations

- use `depends_on` deliberately
- do not assume `depends_on` alone guarantees readiness
- use healthchecks when readiness matters
- keep startup sequencing understandable
- avoid fragile timing assumptions
- prefer deterministic readiness over arbitrary sleeps
- make service failure behavior diagnosable
- document important startup dependencies when they materially affect development or validation

---

## Healthcheck Expectations

- add healthchecks when they improve readiness handling, diagnostics, or developer experience
- keep healthchecks simple and meaningful
- do not add decorative healthchecks that provide no useful signal
- use healthchecks to support dependent services when readiness matters
- ensure healthchecks reflect actual service usefulness, not mere process existence when practical

---

## Security Expectations

- do not hardcode secrets in compose files
- treat local security as important even if the setup is not production
- expose only the ports that are actually needed
- avoid unnecessary privileged container settings
- avoid mounting sensitive host paths carelessly
- keep credentials, tokens, and sensitive config out of logs and committed files
- document when a compose setup is for local convenience only and not production-safe
- do not mistake local usability for production readiness

---

## Development Experience Expectations

- optimize for reproducible local setup
- reduce unnecessary startup friction
- make common developer workflows easy to understand
- keep logs accessible and useful
- make service restart behavior understandable
- prefer setup that helps onboarding rather than relying on oral tradition
- keep the path from clone to running environment as clear as possible

---

## Debuggability Expectations

- startup failures should be diagnosable
- logs should remain usable
- service names should make debugging easier
- commands and overrides should be readable
- health, dependency, and port issues should be traceable without reverse-engineering the whole file
- avoid compose structures that are technically compact but operationally confusing

---

## Stack-Aware Expectations

When relevant, Compose should support the repository stack deliberately.

Examples:
- Kotlin / Spring Boot: backend + PostgreSQL or MongoDB + Redis/Valkey + supporting local services when relevant
- React / Vite: frontend dev server + backend API + supporting services
- NestJS: API + PostgreSQL or MongoDB + Redis/Valkey + local validation dependencies
- OpenAPI-first repositories: mock server, backend, or client validation support when relevant
- Playwright-enabled repos: frontend, backend, database, and supporting services needed for reliable local or CI-style execution

Do not compose services mechanically just for symmetry.

---

## Testing and Validation Expectations

- validate that the composed environment actually starts and works as intended
- validate important service-to-service flows where relevant
- validate readiness behavior when dependent services exist
- validate environment assumptions such as ports, mounts, and required variables
- test the real startup path, not just YAML formatting
- treat green container startup as one signal, not proof the environment is truly usable

---

## Documentation Expectations

Update documentation when relevant, including:
- local setup instructions
- contributor guides
- service startup notes
- environment variable documentation
- architecture docs when local service composition materially reflects system boundaries
- ADRs when meaningful environment or orchestration decisions are made
- troubleshooting notes when recurring environment issues are worth documenting

Do not let compose behavior drift away from documented setup expectations without acknowledgment.

---

## What to Avoid

- giant compose files with unclear purpose
- exposing every service to the host without reason
- hardcoding secrets
- assuming `depends_on` means a service is ready
- relying on arbitrary sleeps instead of deterministic readiness
- overusing overrides or indirection until nobody understands the setup
- using Docker Compose as a fake production orchestration substitute without saying so
- persisting data accidentally when the environment should be disposable
- deleting persistent data accidentally when the environment should retain it
- mounting broad host paths carelessly
- mixing unrelated environment concerns into one compose file without explicit reason
- letting setup drift away from documented developer workflow

---

## Definition of Done

A task using this skill is closer to done when:
- the environment objective is clear
- service responsibilities are understandable
- ports, volumes, networks, and variables are deliberate
- startup dependencies and readiness are handled appropriately
- security-sensitive aspects were considered
- local developer experience was improved or preserved
- startup and debugging remain understandable
- relevant documentation was updated
- known tradeoffs, limitations, or follow-ups were made explicit

---

## Example Tasks

- create a Docker Compose setup for a Kotlin Spring Boot API with PostgreSQL and Redis
- create a local environment for a NestJS API with MongoDB and Redis/Valkey
- orchestrate a React frontend with backend API and database for local development
- improve a fragile compose setup by adding healthchecks and clearer startup behavior
- refactor an oversized compose file into a more understandable structure
- document the local environment behavior and required variables for new contributors
- review whether a compose setup is overexposed, underdocumented, or too coupled to one developer machine

---

## Example Prompts

- "Design a Docker Compose setup for this repository, including service boundaries, ports, healthchecks, and environment variables."
- "Review this docker-compose configuration for clarity, startup reliability, security, and developer experience concerns."
- "Help me refactor this oversized compose file into a cleaner and more maintainable local development setup."
- "Design a local multi-service environment for this stack using Docker Compose, with deliberate persistence, readiness, and debugging support."