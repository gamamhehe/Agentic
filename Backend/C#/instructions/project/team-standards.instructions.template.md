---
name: Team-Standards-Instructions-Template
description: Project-specific team operating rules for review strictness, testing floor, approval gates, and forbidden shortcuts.
---

# Team Standards Instructions

Copy this template to `team-standards.instructions.md` and replace the placeholders with real team rules.

Keep this file focused on team operating standards.
Do not repeat generic architecture or framework guidance that already exists elsewhere.

## Keep here

- review strictness
- minimum testing expectations
- approval-required change types
- forbidden shortcuts
- observability requirements
- naming or design preferences unique to the team

## Do not keep here

- generic clean architecture rules
- general .NET knowledge
- implementation examples
- domain model reference data

## Sections to fill

### Review Mode

- severity threshold:
- architecture violations:
- missing tests:
- observability gaps:

### Required for Feature Completion

- at least one happy-path test:
- validation coverage:
- authorization coverage:
- logging or telemetry requirements:

### Approval Required Before Implementation

- database schema changes:
- new external service integrations:
- auth changes:
- new background jobs:

### Forbidden Shortcuts

- business logic in endpoints:
- direct infrastructure access from Domain or Application:
- skipping tests for risky changes:

### Team Preferences

- preferred result/error handling style:
- preferred DTO conventions:
- preferred dependency registration style:
