# Protect Backend Project Skill

## When to use

Use before merge, release, or hotfix approval when you need a fast safety check focused on project protection.

Trigger phrases:

- protect this project
- run merge gates
- safety check this PR
- pre-merge protection review

## Load this additional guidance

Assume `@Backend-Engineer` already loaded core instructions.

- `instructions/cross-cutting/21-testing.instructions.md`
- `instructions/cross-cutting/22-review-gates.instructions.md`
- touched layer instructions
- `instructions/cross-cutting/20-configuration.instructions.md` when config changes
- `instructions/project/team-standards.instructions.md` when present

## Inputs

- PR diff or changed files
- intent or acceptance criteria
- deployment context (optional)
- risk focus areas (optional)

## Steps

1. Identify touched layers and critical runtime paths.
2. Evaluate all blocking gates from `22-review-gates.instructions.md`.
3. Classify findings as blocking or advisory.
4. Validate test sufficiency for changed behaviors.
5. Return a merge verdict with remediation list.

## Output

1. `Verdict`: `blocked`, `needs-changes`, or `approved-with-notes`
2. `Blocking findings` with gate category and concrete fix
3. `Advisory findings`
4. `Minimum test additions required`
5. `Follow-up guidance updates` (if repeated risks were found)

## Checklist

- [ ] All blocking gates were evaluated
- [ ] Verdict is explicit
- [ ] Blocking findings include remediation
- [ ] Test gaps are concrete and prioritized
- [ ] No style-only noise hides risk findings