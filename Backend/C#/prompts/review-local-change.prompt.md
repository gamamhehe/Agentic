---
description: Review a local backend change or staged patch before merge.
agent: agent
---

Use `@Backend-Engineer` if it is available.

Review the current backend change before it is merged.

Tasks:

1. Identify the change intent and touched layers.
2. Review correctness, regression risk, architecture boundaries, nullability, async behavior, and test coverage before style.
3. Separate blocking issues from advisory improvements.

Return:

1. `Blocking findings`
2. `Important non-blocking findings`
3. `Test gaps`
4. `Guidance gaps`
