# AI Guidance Setup (Cross‑Project Template)

This package separates **agent**, **instructions**, **skills**, and **patterns** so each part has a clear responsibility.

## Responsibilities

### Agent
The agent is the orchestrator.

It:
- identifies the task type
- loads only the relevant instruction files
- loads only the relevant skill files
- uses patterns as implementation references
- creates a plan first for non-trivial work
- suggests missing guidance when the current setup is unclear or incomplete

### Instructions
Instructions define stable rules and boundaries.

They answer:
- what is allowed
- what is required
- what is forbidden
- where code belongs
- what standards must be followed

### Skills
Skills define repeatable task workflows.

They answer:
- when to use a workflow
- what inputs are needed
- what steps to follow
- what output to produce
- what to verify before finishing

### Patterns
Patterns are reusable implementation blueprints and examples.

They answer:
- what good structure looks like
- which classes or wiring are typically used
- example code for the implementation shape

## Precedence

When guidance overlaps or conflicts, use this order:

1. **Instructions**
2. **Skills**
3. **Patterns**

Rules:
- Instructions define policy and boundaries.
- Skills must work within instruction rules.
- Patterns must not override instructions or skills.
- If a skill conflicts with an instruction, the instruction wins and the skill should be updated.
- If a pattern conflicts with an instruction or skill, follow the instruction or skill and update the pattern later.

## Folder Layout

```plaintext
agents/        -> orchestrators
instructions/  -> stable project rules
skills/        -> task workflows
patterns/      -> implementation blueprints and examples
```

## How to add new guidance

### Add or update an instruction when:
- a rule should apply across many tasks
- layer boundaries are unclear
- naming or testing standards need to be enforced
- a policy should remain stable over time

### Add or update a skill when:
- a task is repeated often
- the same execution steps are followed regularly
- the agent needs a reusable checklist for implementation or review

### Add or update a pattern when:
- the team needs a reusable structure example
- code wiring or class layout needs a reference implementation
- a common implementation shape should be documented once and reused

## Practical workflow

1. Start from `agents/Backend.agent.md`
2. Load only the instructions relevant to the current task
3. Load the skills relevant to the current task
4. Use related patterns as reference while implementing or reviewing


## Template notes

- Replace placeholders like `{ProjectName}` and `{Entity}` with real names.
- `instructions/Domain.Project.Instructions.md` is intentionally project-specific and can be removed or replaced per project.
