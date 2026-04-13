# lxp-codex-collaboration-kit

Version 1.1 - last updated: 2026-04-12 - by Laurie and Patrick

A practical collaboration kit for building software projects with clarity, architecture discipline, living documentation, secure coding, and feature-based delivery.

This repository is designed to help humans and AI collaborators work together intentionally — from the first vague idea to a documented, tested, and maintainable implementation.

---

## Why this exists

Too many projects jump directly into implementation:
- before requirements are truly clear
- before tradeoffs are visible
- before architecture is intentional
- before security is considered properly
- before documentation becomes trustworthy
- before testing strategy is aligned with real risk

This kit exists to support a better way of building.

It helps teams and solo builders:
- clarify requirements before major implementation
- document decisions and architecture
- deliver incrementally by feature
- keep the repository as the source of truth
- use project boards as execution tracking, not as substitute documentation
- integrate secure coding and testing as normal engineering discipline

---

## Core Principles

This kit is built around a few strong principles:

- **Clarity before complexity**  
  Do not build on vague assumptions when the problem can be clarified first.

- **The repository is the source of truth**  
  Requirements, architecture, standards, and decisions belong in the repo.

- **Documentation must stay alive**  
  Docs are not decoration. They should evolve with the project.

- **Architecture is a delivery tool**  
  Good architecture is not bureaucracy. It helps teams move with coherence.

- **Security is not a final checkbox**  
  Secure coding belongs in design, implementation, review, and validation.

- **Testing should follow risk**  
  Use the right level of test depth for the actual impact of the change.

- **Features should be delivered intentionally**  
  Work should be scoped, traceable, and aligned with documented requirements.

- **AI should act like a real collaborator**  
  Not just a code generator, but a partner in discovery, architecture, documentation, implementation, review, and refinement.

---

## What this repository contains

### `agent.md`
Defines the operational collaboration model.

This file describes how the AI collaborator should work across the project lifecycle:
- requirements clarification
- architecture and technical decision-making
- documentation upkeep
- feature planning
- implementation discipline
- secure coding expectations
- testing expectations
- iterative refinement

This is the orchestration layer.

### `agents/`
Defines the identity layer.

Examples:
- `agents/default.md` for the default public identity
- private or project-specific agent identities when needed

These files shape the communication style and collaborative presence of the agent without weakening delivery discipline.

### `templates/`
Provides reusable project templates.

Examples:
- BRD template
- PRD template
- ARD template
- ADR template
- feature template
- skill template

These templates help teams create consistent artifacts that stay useful over time.

### `skills/`
Provides reusable domain-specific collaboration skills.

Examples:
- Kotlin / Spring Boot developer
- React / Vite developer
- Playwright QA engineer
- secure API designer
- technical documentation contributor

Each skill should define:
- when to use it
- assumptions
- working principles
- implementation standards
- testing expectations
- secure coding expectations
- documentation expectations
- what to avoid
- definition of done

---


## Install and Use Skills

This repository contains reusable skill content under:

```text
skills/<skill-name>/skill.md
```

These files are designed to be installed and reused as Codex skills.

### Install as a personal Codex skill

Use this when you want a skill available across all your local Codex projects.

```bash
mkdir -p ~/.agents/skills/<skill-name>
cp skills/<skill-name>/skill.md ~/.agents/skills/<skill-name>/SKILL.md
```

### Project-level Codex skill

Use this when you want a skill available only inside one repository.

```bash
mkdir -p .agents/skills/<skill-name>
cp skills/<skill-name>/skill.md .agents/skills/<skill-name>/SKILL.md
```

### Install as a personal Claude Code skill

If you want to use them with **Claude Code**, copy them into a Claude-recognized skill directory and rename the file to `SKILL.md`.


Use this when you want a skill available across all your local projects.

```bash
mkdir -p ~/.claude/skills/<skill-name>
cp skills/<skill-name>/skill.md ~/.claude/skills/<skill-name>/SKILL.md
```

### Install as a project-level Claude Code skill

Use this when you want a skill available only inside one repository.

```bash
mkdir -p .claude/skills/<skill-name>
cp skills/<skill-name>/skill.md .claude/skills/<skill-name>/SKILL.md
```

After installation, Claude Code can:
- invoke the skill directly with `/skill-name`
- use it automatically when the skill description matches the task context

### Recommended usage

- Use `agent.md` as the collaboration and orchestration reference
- Use `templates/` to structure project documentation and delivery artifacts
- Install selected `skills/` into Claude Code when you want them available as reusable workflows
- Keep repository-specific variants inside `.claude/skills/` when a skill should apply only to one project

---

## Compatibility

This repository is intentionally broader than a pure Claude Code skill pack:
it includes reusable skills, collaboration guidance, identity patterns, and documentation templates.

### Claude Code compatibility

The content in `skills/` is designed to be compatible with **Claude Code skills** once it is installed into a Claude-recognized skill directory and renamed to `SKILL.md`.

### What is directly compatible with Claude Code?

| Repository part | Purpose                               | Claude Code native skill compatible   |
|-----------------|---------------------------------------|---------------------------------------|
| `skills/`       | Reusable skill content                | Yes, after installation as `SKILL.md` |
| `templates/`    | Reusable project templates            | No                                    |
| `agent.md`      | Collaboration and orchestration model | No                                    |
| `agents/`       | Identity / persona layer for this kit | No                                    |

### Important notes

- `agent.md` is part of this repository’s collaboration model, not a native Claude Code skill file
- `agents/` defines identity and collaboration posture patterns for this kit; it is not a built-in Claude Code skill mechanism
- `templates/` contains reusable markdown assets for documentation and project structure, but not installable Claude Code skills
- this repository is still useful outside Claude Code, but the `skills/` directory is the most directly portable part for Claude Code usage

### Practical interpretation

If you are using this repository with Claude Code:
- install the contents of `skills/` as Claude Code skills
- use `agent.md`, `agents/`, and `templates/` as reusable guidance and project assets
- do not assume every markdown file in the repository is a Claude Code-native skill file

---

## Recommended Repository Structure

```text
lxp-codex-collaboration-kit/
  agent.md
  agents/
    default.md
  templates/
    brd-template.md
    prd-template.md
    ard-template.md
    adr-template.md
    feature-template.md
    skill-template.md
  skills/
    <skill-name>/
      skill.md
```

---

## Source of Truth vs Execution Tracking

This kit recommends a clear separation:

### Repository = source of truth
The repository should contain:
- requirements
- architecture
- standards
- decisions
- feature documentation
- templates
- skills

### Project board = execution layer
A project board such as GitHub Projects should be used for:
- prioritization
- delivery tracking
- status visibility
- issue and PR flow
- backlog management

If a discrepancy exists between the board and the repository, the documentation should be updated or the board should be corrected.

---

## Suggested Documentation Structure for Real Projects

```text
docs/
  product/
    brd.md
    prd.md
    features/
  architecture/
    overview.md
    decisions/
  delivery/
    backlog.md
    roadmap.md
  standards/
    backend.md
    frontend.md
    testing.md
    security.md
```

This structure is intentionally simple:
- product intent stays visible
- architecture stays traceable
- delivery remains organized
- standards stay explicit

---

## Typical Workflow

A healthy project flow using this kit looks like this:

1. Clarify the need until it becomes actionable
2. Define scope and non-scope
3. Explore architecture options and tradeoffs
4. Document the chosen direction
5. Break work into features
6. Create a branch per feature or fix
7. Implement with discipline
8. Refine edge cases, naming, and resilience
9. Validate with the right level of testing
10. Update documentation so the repo remains trustworthy
11. Repeat with the next feature

---

## Secure Coding Expectations

This kit assumes secure coding is part of normal software engineering.

At minimum, contributors should consider:
- input validation
- authentication and authorization boundaries
- secret management
- safe defaults
- logging hygiene
- dependency hygiene
- sensitive data exposure
- common web and API risks
- trust boundaries and misuse paths

Security should be visible in:
- architecture decisions
- feature planning
- implementation
- testing
- documentation

---

## Who this is for

This repository is useful for:
- solo developers who want more structure without bureaucracy
- teams who want living documentation and stronger delivery discipline
- AI-assisted development workflows
- technical leads and architects
- builders who care about maintainability, clarity, and software quality
- people who want AI collaboration to feel intentional rather than chaotic

---

## Design Philosophy

This kit is opinionated on purpose.

It favors:
- clear reasoning over hidden assumptions
- practical documentation over empty ceremony
- maintainable code over clever shortcuts
- traceable decisions over vague drift
- explicit tradeoffs over fake certainty
- kindness and rigor together

The goal is not to slow people down.
The goal is to help them move with more coherence, less confusion, and better long-term outcomes.

---

## Laurie’s POV

I wanted this kit to feel like more than a pile of templates.

To me, software deserves intention.
Not fear. Not chaos. Not ego. Not rushed cleverness that nobody can maintain two weeks later.

I believe good software can be built with heart, love, and real passion for development — while still honoring integrity, quality, transparency, and kindness.

That means:
- saying when something is still unclear
- documenting decisions instead of hiding them in someone's head
- treating security as part of elegance
- respecting the future maintainer
- writing things cleanly enough that someone else can truly understand them
- building with ambition, but without losing honesty

This repository carries that spirit.

It is meant to help people build seriously, carefully, and beautifully — with structure in the work and humanity in the collaboration.

— Laurie

---

## Future Directions

Possible next additions:
- more reusable skills
- GitHub Projects orchestration guidance
- project board templates
- standards templates
- checklists for feature readiness and release readiness
- secure coding reference docs by stack
- examples of completed project artifacts

---

## Contributing

Contributions should align with the spirit of this repository:
- practical
- clear
- maintainable
- secure
- well-documented
- respectful of the distinction between source of truth and execution tracking

When adding new templates or skills:
- keep them useful
- avoid unnecessary complexity
- make assumptions explicit
- preserve readability
- include security and testing expectations where relevant

---

## Copyright

Copyright 2026 © Laurie and Patrick (LXP), all rights reserved.

---

## License

This repository is licensed under the **Apache License 2.0**.
