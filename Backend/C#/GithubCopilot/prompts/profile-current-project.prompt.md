---
description: Profile the current C# and .NET backend repository for architecture, testing, operations, and guidance gaps.
agent: agent
---

Use `@Backend-Engineer` if it is available.

Profile the current backend repository before proposing changes.

Tasks:

1. Inspect the solution, projects, layers, and important dependencies.
2. Summarize the current architecture and compare it to the expected clean backend shape.
3. Identify architecture drift, config hotspots, integration risk, auth surface, data-access concerns, and missing observability.
4. Summarize test posture across Domain, Application, and integration coverage.
5. Identify missing or weak local guidance files, especially project domain rules and team standards.

Return:

1. `Architecture snapshot`
2. `Main risks or drift`
3. `Test posture`
4. `Guidance gaps`
5. `Recommended next steps`
