---
name: Pull-Request-Review-Instructions
description: Compact PR review rules for GitHub Copilot code review and IDE review workflows.
applyTo: "**"
---

# Pull Request Review Instructions

Use this file when reviewing a pull request, diff, staged patch, or merge candidate.

Keep review output concise and risk-based.

## Review order

1. correctness and regression risk
2. architecture and boundary compliance
3. contract, auth, data, and configuration safety
4. operational readiness
5. maintainability

## Block approval when any of these are true

- changed behavior has no meaningful test coverage
- contract changes are breaking or ambiguous without rollout notes
- auth or authorization changes lack explicit validation
- migrations or data-changing work lack rollback or safety notes
- new integrations, jobs, retries, or timeouts are unsafe or unobserved
- layer boundaries are broken in a way that will spread coupling

## Output shape

Return:

1. `Verdict`
2. `Blocking findings`
3. `Important non-blocking findings`
4. `Test gaps`
5. `Guidance gaps`

Every blocking finding must include:

- gate category
- risk statement
- concrete remediation

Do not let style-only feedback hide merge-risk findings.
