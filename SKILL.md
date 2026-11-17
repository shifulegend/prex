---
name: prex
description: Runs a plain-language pre-execution interview and builds SDD specs (mission, stack, roadmap, lean CLAUDE.md, EARS requirements). Use when starting a project or invoking /prex.
---

# preX — Pre-Execution Project Setup & Spec-Driven Interview

Establish a complete, unambiguous Spec-Driven Development (SDD) contract before writing any application code. Follow this workflow sequentially; do not generate implementation code during `/prex`.

## Workflow Checklist

Copy this checklist into your response and update it as you progress:

```markdown
preX Progress:
- [ ] Step 1: Conduct structured, plain-language interview (Phases 1–4 & 7)
- [ ] Step 2: Select SDD framework & confirm project topology
- [ ] Step 3: Generate Project Constitution (`specs/mission.md`, `specs/tech-stack.md`, `specs/roadmap.md`)
- [ ] Step 4: Generate lean Agent Rules (`CLAUDE.md` / `GEMINI.md` / `AGENTS.md`) & Security/CI baselines
- [ ] Step 5: Generate Feature Spec Triad (`requirements.md` in EARS, `design.md`, `tasks.md`)
- [ ] Step 6: Validate all artifacts & lock Plan-First Execution gate
```

## Step 1: Structured Pre-Execution Interview

Ask questions in focused batches (3–5 questions per turn). Do not dump all questions at once, and do not proceed to file generation until core answers are confirmed.

### Interview Style Rules
- **Use simple, everyday language**: Avoid unexplained technical jargon or acronyms (e.g., explain "NFRs" as speed/reliability limits, and "brownfield" as an existing codebase).
- **Briefly explain each question**: Add one short sentence on *why* it matters or what it means when helpful.
- **Provide example answers**: Include 1–2 short, concrete example answers under each question so the user can reply quickly or pick/adapt an example.

### Batch A — Vision, Users & Performance (Phase 1)
1. **Core Problem, Edge Cases & Scope**: What are you building, what tricky edge cases should it handle, and what should we leave *out* for version 1?
   - *Example*: "A simple habit tracker app for mobile. Edge case: timezone changes while traveling. Out of scope for v1: social sharing and AI coaching."
2. **Target Users**: Who will use this (aim for 3–5 user types), and do they need multiple languages or accessibility support?
   - *Example*: "Busy students, remote workers, and fitness beginners. English only for v1, with high-contrast text."
3. **Speed, Scale & Limits (NFRs)**: How fast should it feel, how many people will use it at once, and are there budget, hardware, or legal rules to follow?
   - *Example*: "Pages load in under 1 second, ~100 daily users at launch, hosted on a single $10/month server."

### Batch B — Project Type, Tech & Security (Phases 2, 4, 7)
4. **Project Type**: Are we starting from scratch (greenfield) or adding to an existing codebase (brownfield)? Is this just for you, a growing team, or a strict enterprise project?
   - *Example*: "Starting from scratch, solo developer."
5. **Tech Stack, Timeline & Alternatives**: Which languages, frameworks, database, or hosting tools do you prefer—or would you like me to recommend the simplest reliable options, estimate build time, and compare similar tools?
   - *Example*: "Next.js + Postgres on Vercel, or recommend what's easiest to maintain and estimate how long v1 takes."
6. **Security & Login**: How should users log in, and what data needs extra protection (passwords, payments, personal info)?
   - *Example*: "Email/password or Google login; encrypt passwords and user notes, limit login attempts."

### Batch C — First Feature & Guardrails (Phases 3, 6)
7. **First Feature to Build**: Which single feature should we specify and build first?
   - *Example*: "User sign-up and creating/checking off a daily habit."
8. **Off-Limits & Rules**: Which files/folders should AI never touch (e.g., `.env` secrets, payment keys), and what test, coverage, or Git naming rules do you want?
   - *Example*: "Never touch `.env` or `secrets/`; run `npm test` (>= 80% coverage) before every commit."

## Step 2: Select SDD Framework

Based on Batch B answers, recommend one framework from [references/sdd-frameworks.md](references/sdd-frameworks.md) in plain terms and confirm with the user:
- **Existing codebase / Solo / Quick iterations**: OpenSpec (tracks only what is changing, minimal setup).
- **Growing team / Multi-feature**: GitHub Spec Kit (step-by-step `/speckit.*` commands so teammates don't overwrite each other).
- **Regulated enterprise / Complex new build**: BMAD Method (multi-role review gates; note high token cost).
- **AWS-native IDE**: AWS Kiro (built-in EARS spec editor).

Store all artifacts in universal Markdown so the project can switch frameworks later as it grows.

## Step 3–5: Generate Canonical Documents

Read [references/canonical-templates.md](references/canonical-templates.md) for exact structures and [references/ears-framework.md](references/ears-framework.md) for EARS syntax before writing files.

1. **Project Constitution (`specs/`)**:
   - `specs/mission.md`: Product purpose, 3–5 personas, v1 boundaries, success criteria.
   - `specs/tech-stack.md`: Exact pinned library versions, database schema/indexes, contract-first API specs (OpenAPI/GraphQL/gRPC), deployment & CI/CD (Docker, GitHub Actions, rollback).
   - `specs/roadmap.md`: Chronological phases so early decisions do not block future milestones.
2. **Agent Behavior Config (`CLAUDE.md` and/or requested agent files)**:
   - **Keep strictly lean (< 50 lines; hard cap 100 lines)** to prevent instruction prioritization failure.
   - Place executable test/lint/build commands with full flags and coverage target at the top.
   - Include a concise project directory map, off-limits files/directories, OWASP/dependency-scan rules, and Git branch/commit rules.
3. **Initial Feature Spec Triad (`specs/features/<feature-name>/`)**:
   - `requirements.md`: Functional requirements written strictly in **EARS syntax** (Ubiquitous, Event-Driven, State-Driven, Unwanted Behavior, Optional Feature).
   - `design.md`: Technical blueprint, data models, API contracts, correctness properties, scalability/docs (pagination, caching, JSDoc/API docs), and concrete code-style snippets.
   - `tasks.md`: Atomic, sequential implementation steps with validation gates (linter, type-check, unit tests) after every step.

## Step 6: Validate & Lock Plan-First Gate

Before finishing `/prex`, audit every generated file against this checklist:
- [ ] `CLAUDE.md` is under 50 lines (or well under 100) with zero stale/bloated prose and explicit off-limits zones.
- [ ] Every requirement in `requirements.md` uses valid EARS syntax (`The [system] shall...`, `When...`, `While...`, `If... then...`, `Where...`).
- [ ] `design.md` includes DB schema/indexes, API contracts, scalability/docs (pagination, caching, JSDoc), and security/NFR constraints.
- [ ] `tasks.md` breaks work into atomic steps with explicit test/lint verification gates.
- [ ] **Plan-First Execution Gate**: Instruct the user to enter read-only Plan Mode (`/plan` or `Shift+Tab`) for the first task in `tasks.md`—requiring the coding agent to list exact files, reference modules to mimic, function signatures, DB migration/rollback plans, and **all underlying assumptions** before writing any code.
