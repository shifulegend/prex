# Canonical Document Templates

## Contents
- [1. `specs/mission.md`](#1-specsmissionmd)
- [2. `specs/tech-stack.md`](#2-specstech-stackmd)
- [3. `specs/roadmap.md`](#3-specsroadmapmd)
- [4. `CLAUDE.md` (Lean Agent Rules)](#4-claudemd-lean-agent-rules)
- [5. Feature Triad (`requirements.md`, `design.md`, `tasks.md`)](#5-feature-triad)

---

## 1. `specs/mission.md`

```markdown
# Project Mission: [Project Name]

## Purpose & Core Problem
- [1–2 sentences on what the product does and why it exists]
- **Critical Edge Cases**: [Key edge cases to handle in v1]

## Target User Personas (3–5)
1. **[Persona Name]**: [Role, goal, key constraint]
2. **[Persona Name]**: [Role, goal, key constraint]
3. **[Persona Name]**: [Role, goal, key constraint]

## Scope Boundaries
- **In Scope (v1)**: [Bullet list]
- **Out of Scope (v1)**: [Bullet list]

## Non-Functional Requirements (NFRs)
- **Performance / Latency**: [Targets]
- **Scale / Concurrency**: [Targets]
- **Accessibility & i18n**: [Standards, e.g., WCAG AA, supported locales]
- **Compliance**: [Standards, e.g., GDPR, SOC2, OWASP]
```

## 2. `specs/tech-stack.md`

```markdown
# Technical Stack & Architecture: [Project Name]

## Pinned Stack & Feasibility
- **Frontend**: [Framework + exact version]
- **Backend**: [Runtime/Framework + exact version]
- **Database & Caching**: [DB + version, cache + version]
- **Infrastructure & CI/CD**: [Docker, GitHub Actions, hosting, rollback strategy]
- **Build-Time Estimate & Reference Architectures**: [Estimated timeline + notes]

## System Architecture & Data Flow
- [Component dependency summary / sequence flow]

## Database Schema & Indexes
- [Tables, primary/foreign keys, critical indexes]

## API Contract
- [Link or inline OpenAPI YAML / GraphQL / gRPC contract]

## Security Baseline
- **AuthN / AuthZ**: [e.g., JWT, OAuth2, bcrypt/argon2]
- **Data Protection**: [TLS in transit, encryption at rest, input validation, rate limiting]
```

## 3. `specs/roadmap.md`

```markdown
# Implementation Roadmap: [Project Name]

## Phase 1: Foundation & Core Infrastructure
- [ ] [Milestone + exit criteria]

## Phase 2: Core Features
- [ ] [Milestone + exit criteria]

## Phase 3: Hardening, Observability & Launch
- [ ] [Milestone + exit criteria]
```

## 4. `CLAUDE.md` (Lean Agent Rules — Target < 50 Lines)

```markdown
# [Project Name] — Agent Rules

## Commands & Coverage (Run Before Commit)
- Test: `[exact command with flags, e.g., pytest -v --cov=src]` (Target: `>= [XX]%`)
- Lint/Typecheck: `[exact command]`
- Build: `[exact command]`

## Directory Map & Canonical Context
- Layout: `src/` (app), `tests/` (test suite), `specs/` (mission, tech-stack, roadmap)

## Code & Git Standards
- [Concise naming/style rule or pointer to reference file]
- Branches: `[e.g., feat/<id>-<slug>]`; Commits: `[Conventional Commits]`

## Hard Boundaries (Never Modify Without Explicit Approval)
- Secrets & env files: `.env*`, `secrets/`
- Vendor & build artifacts: `node_modules/`, `dist/`
- Auth & CI pipelines: `.github/workflows/`, `[auth module path]`
- Security: Follow OWASP top-10; run dependency audit before adding packages.
```

## 5. Feature Triad

### `specs/features/<feature>/requirements.md`
```markdown
# Requirements: [Feature Name]

## User Stories
- As a [persona], I want [capability] so that [outcome].

## EARS Functional Requirements
- **REQ-01 (Ubiquitous)**: The [system] shall [action].
- **REQ-02 (Event-Driven)**: When [trigger], the [system] shall [action].
- **REQ-03 (Unwanted Behavior)**: If [error condition], then the [system] shall [action].
```

### `specs/features/<feature>/design.md`
```markdown
# Design Contract: [Feature Name]

## Architecture & Component Changes
- [Exact files/modules to create or update]

## Data Model & Migration Plan
- [Schema changes, SQL up/down migrations, rollback steps]

## API / Interface Contract
- [Endpoints, request/response schemas, status codes]

## Scalability, Docs & Style Reference
- **Pagination & Caching**: [Strategy]
- **Inline & API Docs**: [e.g., JSDoc / OpenAPI update plan]
- **Reference Module**: [Path to existing module for naming/style conventions]
```

### `specs/features/<feature>/tasks.md`
```markdown
# Tasks: [Feature Name]

> Enter Plan Mode (`/plan` or `Shift+Tab`) before executing each task. List exact files, reference modules to mimic, signatures, and all assumptions for approval first.

- [ ] **Task 1**: [Atomic unit, e.g., Add DB migration] → Gate: `[migration + test command]`
- [ ] **Task 2**: [Atomic unit, e.g., Implement API endpoint] → Gate: `[lint + integration test command]`
- [ ] **Task 3**: [Atomic unit, e.g., Build UI component] → Gate: `[typecheck + unit test command]`
```
