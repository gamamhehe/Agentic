---
description: Review a backend pull request for correctness, merge risk, architecture, and test coverage.
agent: agent
---

Use `@Global` if it is available.

Review this backend pull request with a correctness-first, merge-risk-focused workflow.

Tasks:

1. Read the PR intent first.
2. Review correctness, regression risk, architecture boundaries, contract safety, auth, data, config, and operational readiness.
3. Check whether tests cover the changed behavior and whether rollout notes are missing.
4. Separate blocking findings from advisory feedback.

Return:

1. `Verdict`
2. `Blocking findings`
3. `Important non-blocking findings`
4. `Test gaps`
5. `Guidance gaps`
