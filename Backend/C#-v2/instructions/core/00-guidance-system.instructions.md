---
name: Guidance System Instructions
description: Explains how agents, instructions, skills, and patterns work together and how to load them without duplicating context.
applyTo: "**"
---

# Guidance System Instructions

## Purpose

This file is the entry rulebook for the guidance repository.

It explains the role of each artifact type and the order they must be used in so the agent does not load everything blindly, repeat the same rules, or confuse examples with policy.

## Artifact Roles

| Artifact | Role | Use for | Must it be followed? |
|---|---|---|---|
| `agents/` | entry behavior | task triage, loading strategy, workflow | yes |
| `instructions/` | policy | boundaries, rules, naming, architecture | yes |
| `skills/` | workflow | step-by-step execution for a task type | yes, but only within instruction rules |
| `patterns/` | examples | implementation shape, sample code, folder blueprints | reference only |

## Loading Order

Always load guidance in this order:

1. **Agent**
2. **Relevant instructions**
3. **Relevant skills**
4. **Relevant patterns**

## Conflict Rules

- If two files overlap, the more specific instruction wins over the more general one
- A layer instruction wins over a pattern
- A cross-cutting instruction applies across all touched layers
- A skill must never override an instruction
- A pattern must never be treated as policy

## Default Loading Strategy

Do not load the whole repository by default.

Instead:

1. identify the task type
2. identify the impacted layers
3. load the smallest useful set of instructions
4. load one or more matching skills
5. consult only the patterns needed for implementation details

## Recommended Instruction Sets by Task

### API endpoint work
- `instructions/core/01-architecture.instructions.md`
- `instructions/layers/13-webapi.instructions.md`
- `instructions/layers/11-application.instructions.md`
- `instructions/core/02-naming.instructions.md`

### Application use-case work
- `instructions/core/01-architecture.instructions.md`
- `instructions/layers/11-application.instructions.md`
- `instructions/core/02-naming.instructions.md`

### Domain model work
- `instructions/core/01-architecture.instructions.md`
- `instructions/layers/10-domain.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/project/Domain.Project.instructions.template.md` only when the project has domain-specific rules

### Infrastructure work
- `instructions/core/01-architecture.instructions.md`
- `instructions/layers/12-infrastructure.instructions.md`
- `instructions/core/02-naming.instructions.md`
- `instructions/cross-cutting/20-configuration.instructions.md` when config is involved

### Review or refactor
- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`
- add the touched layer instructions
- `instructions/cross-cutting/21-testing.instructions.md` when behavior safety matters

## Repository Design Rules

- Keep each file focused on one job
- Avoid restating the same rules in multiple files
- Put policy in instructions, not skills
- Put examples in patterns, not instructions
- Put step-by-step workflow in skills, not agents
- Keep filenames stable and descriptive so agents can reference them directly

## When to Add New Files

Add a new file only when one of these is true:

- a new layer or cross-cutting concern has unique policy
- a workflow is repeated enough to deserve a reusable skill
- a pattern is needed to show a stable implementation blueprint
- the project has domain-specific rules that do not belong in generic guidance

## When to Update Existing Files

Prefer updating an existing file when the new guidance is just:
- an extra rule in the same concern
- a clarified example
- a small workflow improvement
- a project-specific extension of an existing generic rule

