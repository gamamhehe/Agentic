# Refactor Plan - Backend Agent as the Single Working Entry Point

> Status: Updated from resolved decisions
> Scope: `Backend/C#/` only

---

## Goal

Refactor the backend guidance so the system works through `Backend/C#/agents/Backend.agent.md` as the real entry point for coding work.

The main goal is no longer "developer and leader productivity" in general.
The goal is to make the backend agent:

1. the single place that developers rely on to start work
2. complete enough that it does not depend on `copilot-instructions.md` for important behavior
3. clear about instruction, skill, and pattern usage
4. governable by team leads through agent-facing guidance, not by expecting developers to read extra files

---

## Confirmed Decisions

These decisions are already resolved and should be treated as plan inputs, not open questions.

| # | Decision |
| --- | --- |
| 1 | Merge the useful content of `Backend/C#/copilot-instructions.md` into `Backend/C#/agents/Backend.agent.md`, then leave `copilot-instructions.md` blank or minimal. |
| 2 | Do not optimize for developers reading standalone instruction entry files directly. |
| 3 | Assume developers work through `Backend/C#/agents/Backend.agent.md`; that file is the real operational surface. |
| 4 | The deleted item is out of scope and should be removed from the plan. |
| 5 | Patterns are for code samples and implementation reference only, not policy or onboarding. |
| 6 | "Leaders can't govern the AI" should be solved with an agent-facing governance plan and an example template. |
| 7 | The stale cross-reference issue should simply be fixed. |
| 8 | Add fields only where they materially help the agent behave better. |
| 9 | Remove the old item 9 from the plan. |
| 10 | Remove the old item 10 from the plan. |

---

## Updated Problem Statement

The current issue is not mainly missing documentation for humans.
The real issue is that the backend guidance is split across files in a way that does not match how coding actually starts.

### Current gaps

1. `Backend/C#/agents/Backend.agent.md` is the actual execution entry point, but some core guidance still lives in `Backend/C#/copilot-instructions.md`.
2. The plan previously assumed developers would read instruction files directly, but in practice the agent should load and apply them.
3. The old plan treated patterns too broadly; they should be positioned only as code examples and reference material.
4. Team-lead control is underspecified: there is no clear agent-facing way to define review strictness, required checks, or "done" criteria.
5. At least one stale reference still exists and should be corrected directly instead of debated.

---

## Proposed Changes

### A. Make `Backend.agent.md` self-sufficient

Update `Backend/C#/agents/Backend.agent.md` so it includes the important guidance currently duplicated or implied elsewhere:

- guidance precedence
- task classification
- when to load instructions
- when to load skills
- how to use patterns
- plan-first behavior for non-trivial work
- when to stop for approval

Result:
The backend agent becomes the one file that actually governs backend coding behavior.

### B. Reduce `copilot-instructions.md` to a blank or minimal stub

After merging the useful content into the backend agent, reduce `Backend/C#/copilot-instructions.md` so it does not carry important logic anymore.

Recommended end state:

- either blank by design
- or a very short note that points to `agents/Backend.agent.md`

Result:
No important backend behavior depends on a secondary entry file.

### C. Reframe patterns as reference-only

Update planning and wording so patterns are clearly described as:

- code sample references
- implementation blueprints
- non-authoritative compared with instructions and skills

Result:
The agent uses patterns to shape code, not to infer policy.

### D. Fix stale references directly

Correct the outdated `CodePatterns.md` / `DomainPatterns.md` reference mismatch and any related stale wording in backend guidance.

Result:
The guidance becomes internally consistent without introducing more structural debate.

### E. Add an agent-facing governance layer for leads

To solve "leaders can't govern the AI", add a lightweight governance file that the backend agent can load when present.

Recommended file:
`Backend/C#/instructions/TeamStandards.instructions.md`

This file should let a lead define:

- required review strictness
- mandatory vs optional patterns
- minimum testing expectations
- forbidden shortcuts
- approval-required change types
- feature completion criteria

Result:
Leads govern the agent by configuring guidance the agent reads, not by expecting every developer to remember extra rules.

---

## Team Lead Governance Plan

This is the concrete plan for solving the leadership-control gap.

### Step 1

Create `TeamStandards.instructions.md` as an optional project-level instruction file.

### Step 2

Teach `Backend.agent.md` to load it only when present and only when relevant.

### Step 3

Use simple fields that are easy for both humans and AI to follow.

### Step 4

Treat this file as agent-facing policy, not as a tutorial.

### Step 5

Keep project-specific domain rules separate from team operating rules.

---

## Sample Governance Template

This is a sample shape for the team-lead control file.

```md
# Team Standards

## Review Mode

- severity threshold: blocking
- architecture violations: blocking
- naming inconsistencies: advisory
- missing observability on critical flows: blocking

## Required For Feature Completion

- at least one happy-path test
- validation behavior covered
- logging or telemetry added for critical paths
- cancellation token handled in async application and infrastructure code

## Approval Required Before Implementation

- database schema changes
- new external service integrations
- background jobs
- authentication or authorization changes

## Forbidden Shortcuts

- business logic in endpoints
- direct infrastructure access from domain
- skipping tests for non-trivial handlers

## Team Preferences

- prefer explicit request and response models
- prefer MediatR-based use cases
- prefer result-based error handling where already used
```

This is enough to let a lead govern the agent in a practical way.

---

## What Changed From the Old Plan

- Removed the assumption that developers read instruction entry files directly.
- Removed deleted or no-longer-needed items from the decision list.
- Removed bootstrap and README items that are no longer part of the chosen direction.
- Repositioned patterns as code-sample references only.
- Recentered the plan around `Backend.agent.md` as the real execution surface.
- Added a concrete team-governance approach with a sample template.

---

## Execution Order

1. Merge important `copilot-instructions.md` content into `Backend/C#/agents/Backend.agent.md`.
2. Blank or minimize `Backend/C#/copilot-instructions.md`.
3. Fix stale backend guidance references.
4. Add `TeamStandards.instructions.md` template if we want lead governance now.
5. Do a final wording pass so plans, instructions, and patterns all match the new model.

---

## Out of Scope

- Frontend guidance
- Rebuilding the whole instruction system
- Turning patterns into policy files
- Any work for deleted items 4, 9, and 10
