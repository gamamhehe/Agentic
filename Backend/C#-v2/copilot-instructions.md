# Copilot Instructions

Start with `instructions/core/00-guidance-system.instructions.md`.

Then:

1. Identify the task type and impacted layers
2. Load only the relevant instruction files
3. Load the matching skill files
4. Use pattern files only as reference examples
5. Make a short plan before non-trivial work
6. Keep architecture boundaries, naming, testing, and maintainability consistent with the loaded guidance
7. If guidance is missing, contradictory, or duplicated, flag it and suggest the smallest useful improvement

Default core files:
- `instructions/core/00-guidance-system.instructions.md`
- `instructions/core/01-architecture.instructions.md`
- `instructions/core/02-naming.instructions.md`

Do not load the full repository unless the task genuinely spans most of it.
