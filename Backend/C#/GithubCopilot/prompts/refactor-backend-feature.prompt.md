---
description: Refactor a backend feature while preserving behavior and protecting architecture boundaries.
agent: agent
---

Use `@Global` if it is available.

Refactor the targeted backend feature without changing intended behavior.

Tasks:

1. State the behavior that must remain unchanged.
2. Identify the touched layers and any current architecture problems.
3. Refactor for clearer boundaries, lower duplication, and easier maintenance.
4. Call out approval gates before changing contracts, auth, data, integrations, or jobs.
5. Recommend or add regression coverage for risky paths.

Return:

1. `Behavior-preservation notes`
2. `Refactor summary`
3. `Boundary improvements`
4. `Test updates or gaps`
