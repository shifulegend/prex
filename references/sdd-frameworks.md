# Adaptive SDD Framework Selection Guide

Select the Spec-Driven Development (SDD) framework that matches the project's scale, codebase age, and team structure.

## Framework Comparison

| Framework | Optimal Use Case | Unit of Work | Token Cost | Key Differentiator |
| :--- | :--- | :--- | :--- | :--- |
| **OpenSpec** | Brownfield modernization, iterative fixes, solo developers | The Change (Deltas) | Low | Minimal overhead; isolates proposed changes as requirement deltas without repo reorganization. |
| **GitHub Spec Kit** | Scaling teams, new features, balanced structure | The Feature | Medium | Phase-gated slash-command workflow (`/speckit.specify`, `/speckit.plan`, `/speckit.tasks`) with numbered feature isolation. |
| **BMAD Method** | Greenfield enterprise, regulated industries, complex scope | The Intent / Product | Very High (~31k+ tokens/run) | Multi-agent persona simulation (Analyst, PM, Architect, QA) with strict human-in-the-loop gates. |
| **AWS Kiro** | Deep AWS ecosystem integration | The Spec | Variable | Dedicated IDE generating EARS-based requirements, design, and tasks natively. |

## Selection & Migration Rules

- **Start Lean**: Solo or brownfield projects should default to **OpenSpec** to avoid bureaucratic bottlenecks.
- **Scale Up**: Transition to **GitHub Spec Kit** when multiple engineers or parallel agents work on concurrent features.
- **Enterprise / Regulated**: Reserve **BMAD** for high-compliance greenfield systems where auditability outweighs token cost and latency.
- **Portability**: Store all specs in plain Markdown (`specs/`) so artifacts remain tool-agnostic across framework transitions.
