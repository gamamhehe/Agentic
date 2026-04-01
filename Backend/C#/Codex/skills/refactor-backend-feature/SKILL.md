---
name: refactor-backend-feature
description: Refactor backend code in a C# and .NET repository while preserving intended behavior.
---

# Refactor Backend Feature

Assume Codex has already read the repository `AGENTS.md`.

## When to use

Use this skill when the primary goal is structural improvement, simplification, or boundary cleanup without changing intended behavior.

## Primary boundary

Lifecycle boundary: behavior-preserving structural change.

## Out of scope

- introducing new feature behavior without calling that out explicitly
- project bootstrap work
- PR-level approval review

## Typical inputs

- code area to simplify or restructure
- architectural smell or coupling to reduce
- behavior that must remain stable
- known tests or risks around the refactor

## Workflow

1. State the behavior that must remain unchanged.
2. Identify the coupling, duplication, or clarity problem being addressed.
3. Refactor in small, explainable steps that preserve boundaries.
4. Add or strengthen tests when existing coverage is too weak to protect the refactor.
5. Call out any residual risks or follow-up cleanup that should stay separate.

## Output

- refactor summary
- preserved behavior statement
- boundary or maintainability improvements
- verification and test notes

## Escalate to / pair with

- pair with `write-tests` when regression protection is weak
- pair with `review-backend-change` when the user wants a post-refactor quality review
