---
name: conventional-commits
description: "Use when writing Git commit messages or PR titles."
metadata:
  category: collaboration
---

# Conventional Commits

Follow the Conventional Commits specification.

## Format

<type>(<scope>): <description>

## Types

- `feat` — New functionality
- `fix` — Bug fix
- `perf` — Performance improvement
- `refactor` — Code restructuring without behavior changes
- `docs` — Documentation
- `test` — Tests
- `build` — Build system or dependencies
- `ci` — CI/CD changes
- `chore` — Maintenance

## Rules

- Use lowercase types and imperative descriptions.
- Keep the subject concise (preferably under 72 characters).
- Use a scope when it meaningfully identifies the affected subsystem.
- Use `!` for breaking changes and explain them in the commit body.
- Describe what changed, not the development process.
- Match existing repository conventions.
- Never claim a change is complete unless it is implemented.
