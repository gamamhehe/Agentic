---
name: protect-backend-project
description: Run a fast merge-gate protection review for a C# and .NET backend. Use before merge, release, or hotfix approval when a concise safety verdict is needed.
---

# Protect Backend Project

## When to use

Use this skill before merge, release, or hotfix approval when you need a fast safety check focused on project protection.

## Load this guidance

- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/cross-cutting/22-review-gates.instructions.md`
- `instructions/cross-cutting/23-pr-review.instructions.md`
- touched layer instructions
- `instructions/cross-cutting/20-configuration.instructions.md` when config changes
- `instructions/project/team-standards.instructions.md` when present

## Inputs

- PR diff or changed files
- intent or acceptance criteria
- deployment context when available
- risk focus areas when available

## Workflow

1. Identify touched layers and critical runtime paths.
2. Evaluate all blocking gates from `22-review-gates.instructions.md`.
3. Classify findings as blocking or advisory.
4. Validate test sufficiency for changed behaviors.
5. Return a merge verdict with remediation guidance.

## Output

1. `Verdict`
2. `Blocking findings`
3. `Advisory findings`
4. `Minimum test additions required`
5. `Follow-up guidance updates`
