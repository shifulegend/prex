# Contributing to prex

Thank you for your interest in contributing to `shifulegend/prex`!

## Pull Requests

- All Pull Requests must target the `main` branch directly (fork the repository, create a branch for your changes, and open a PR against `main`).

## Commit Messages

Follow **Conventional Commits** for all commit messages:

- `feat:` — A new feature or capability
- `fix:` — A bug fix
- `docs:` — Documentation changes
- `chore:` — Maintenance or tooling tasks
- `refactor:` — Code or structure refactoring without changing behavior
- `test:` — Adding or updating tests or evaluations

## Required PR Checks

Before submitting a Pull Request, ensure your changes satisfy all of the following checks:

1. **Skill Structure & Size**: Keep `SKILL.md` under 500 lines and keep references one-level-deep in `references/`.
2. **YAML Frontmatter Description**: Keep the YAML frontmatter `description` at or under 200 characters, written in third-person POV, stating what the skill does and when to use it.
3. **Evaluations**: Test changes against all scenarios in `evals/evals.json` across target Claude models.
4. **Security & Privacy**: Never include secrets, API keys, or personal data.
