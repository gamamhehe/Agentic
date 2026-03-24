# Refactor Plan — Agentic Guidance System for C# Developers & Leaders

> Status: Draft — open for discussion
> Scope: `Backend/C#/` only (Frontend is WIP and out of scope for now)

---

## Goal

Transform this repo from a **guidance archive** into a **developer and team leader productivity tool** that:

1. Is immediately usable on a real C# project with zero setup confusion
2. Gives a team lead clear control and visibility over what the AI will and won't do
3. Teaches the patterns it enforces, rather than just enforcing them silently
4. Scales cleanly from solo developer to team use
5. Grows incrementally as new needs arise without requiring full rewrites

---

## Problem Statement

The current state is well-structured but has several gaps for real-world use:

| #   | Problem                                                                                                                                                                             | Impact                                                          |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------- |
| 1   | `copilot-instructions.md` is a generic placeholder — developers must manually fill in blanks                                                                                        | First install feels incomplete; AI starts with degraded context |
| 2   | Skills are workflow guides but have no "quick-start" summary — a developer must read the whole file to know what happens                                                            | Slows down adoption                                             |
| 3   | No skill exists for common senior-developer tasks: **Architecture Review**, **Breaking Change Analysis**, **Performance Review**                                                    | Limits value for tech leads                                     |
| 4   | `Domain.Project.Instructions.md` is hardcoded to one project (Guidance Archive) — a new user sees domain rules for the wrong project                                                | Confusing for reuse                                             |
| 5   | Pattern files have no difficulty/complexity signal — a junior developer and a tech lead get the same undifferentiated content                                                       | No progressive disclosure                                       |
| 6   | No onboarding path for team leads — nothing explains how to configure the AI for a team, set review standards, or define what "done" means                                          | Leaders can't govern the AI                                     |
| 7   | `CodePatterns.md` is now effectively `DomainPatterns.md` (renamed last session) — but `Architecture.instructions.md` still references it as "Background jobs and shared primitives" | Stale cross-reference                                           |
| 8   | No **HangfirePatterns.md** reference in `Architecture.instructions.md` Related Pattern Files table                                                                                  | Pattern is invisible to agent at architecture-load time         |
| 9   | `README.md` install prompts copy `Domain.Project.Instructions.md` as-is — a new project gets the wrong domain out of the box                                                        | Incorrect setup                                                 |
| 10  | No `BootstrapAgenticGuidance.skill.md` update path — `skills/BootstrapAgenticGuidance.skill.md` exists at repo root but is never referenced from the Backend README                 | Broken discovery                                                |

---

## Proposed Changes

### Group A — Quick Fixes (no structural change, low risk)

These are safe, targeted corrections.

| ID  | File                                 | Change                                                                                                                              |
| --- | ------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------- |
| A1  | `Architecture.instructions.md`       | Fix Related Pattern Files table: `CodePatterns.md` → `DomainPatterns.md`, add `HangfirePatterns.md` row                             |
| A2  | `Backend/C#/README.md`               | Update install prompt to NOT copy `Domain.Project.Instructions.md` — instead instruct developer to create their own from a template |
| A3  | `Backend/C#/copilot-instructions.md` | Replace placeholder comments with a concrete filled-in example and clear inline instructions for what to change                     |
| A4  | `Domain.Project.Instructions.md`     | Add a prominent `> ⚠️ Project-specific — replace with your own domain model` header (already exists but could be stronger)          |

---

### Group B — New Skills for Tech Leads (additive, no renames)

Three high-value skills that don't exist yet and would specifically help senior developers and team leads.

| ID  | File                                           | Purpose                                                                                                                                                                                                         |
| --- | ---------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| B1  | `skills/ReviewArchitectureCompliance.skill.md` | Deep architecture review: boundary violations, layer leaks, DI correctness, pattern deviations. More thorough than `ReviewBackendChange`.                                                                       |
| B2  | `skills/AnalyseBreakingChange.skill.md`        | Given a proposed change, identify API contract breaks, EF Core migration risks, behavior regressions, dependent service impacts.                                                                                |
| B3  | `skills/PlanFeature.skill.md`                  | Given a feature request, produce a structured implementation plan: layers touched, CQRS decomposition, infrastructure needs, test strategy, risks. Oriented at a lead reviewing AI output or planning a sprint. |

These complement the existing set without replacing anything:

```
Current skills:           New skills:
CreateEndpoint            ReviewArchitectureCompliance  ← deeper than ReviewBackendChange
CreateUseCase             AnalyseBreakingChange         ← new concern
UpdateDomainModel         PlanFeature                   ← lead-oriented planning
ImplementInfrastructure
WriteTests
ReviewBackendChange
RefactorBackendFeature
AddRequestTracking
ConfigureApplicationSettings
```

---

### Group C — Team Lead Configuration Layer (new, additive)

A thin new layer that gives a team lead a place to configure what the AI enforces for their team, without modifying core guidance files.

**Proposed new file: `instructions/TeamStandards.instructions.md`**

This file would let a lead define:

- which patterns are mandatory vs optional for their team
- review severity levels (blocking vs advisory)
- team-specific naming overrides
- what "done" means for a feature (e.g. requires integration test, requires observability wiring)
- which layers a junior developer should not touch without review

This stays **empty / commented out** in the repo and is filled in per-project. It sits between generic guidance and project-specific domain rules.

---

### Group D — Structural Renames

Renames to fix naming inconsistencies discovered in earlier sessions.

| ID  | Current name                         | Proposed name                             | Reason                                                            |
| --- | ------------------------------------ | ----------------------------------------- | ----------------------------------------------------------------- |
| D1  | `patterns/CodePatterns.md`           | `patterns/DomainPatterns.md`              | Content is `Result<T>` at `Domain/Common/` — name matches content |
| D2  | `Backend/C#/copilot-instructions.md` | No rename — but content overhaul (see A3) | File name is correct, content is the issue                        |

> Note: D1 requires updating all cross-references in instruction files, skill files, and `Architecture.instructions.md`. A find-and-replace is sufficient.

---

### Group E — Developer Experience: Quick-Start Summaries in Skills (optional, low priority)

Add a `## Summary` one-liner at the top of each skill file so a developer can read one sentence and decide whether to load the full file.

Example for `CreateEndpoint.skill.md`:

```markdown
## Summary

Create a Minimal API endpoint, wire it to a MediatR command or query, declare OpenAPI metadata, and verify the handler is thin.
```

This is cosmetic and low-risk but improves daily usability.

---

## Decisions Needed

| #   | Question                                                                             | Options                                                                                                                   |
| --- | ------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Rename `CodePatterns.md` → `DomainPatterns.md`?**                                  | Yes (correct + consistent) / No (too disruptive to ongoing projects that already pulled the files)                        |
| 2   | **Add `TeamStandards.instructions.md`?**                                             | Yes, as an empty template / Yes, with example content / Not yet                                                           |
| 3   | **Which new skills to build first?**                                                 | All three (B1–B3) / Just `PlanFeature` (highest lead value) / Just `ReviewArchitectureCompliance` (closes the review gap) |
| 4   | **Fix the `copilot-instructions.md` placeholder?**                                   | Yes, overhaul with a concrete example / Yes, minimal fix / Leave as-is                                                    |
| 5   | **Update the bootstrap install prompt to exclude `Domain.Project.Instructions.md`?** | Yes (correct) / No, keep it and rely on the warning header                                                                |

---

## What is NOT in scope for this refactor

- Frontend (`Frontend/Vue/`) — it is WIP and should be tackled separately
- Changing the two-tier model (user space / project space) — it is solid
- Changing the agent behavior logic in `Backend.agent.md` — the workflow is correct
- Any changes to the `agentic.instructions.md` meta-governance file — just updated last session

---

## Suggested Execution Order (if all approved)

```
Phase 1 — Clean up (A1–A4, D1)           ← safe, no new content
Phase 2 — New skills (B1–B3)             ← additive, no breakage
Phase 3 — Team lead layer (C)            ← new file, no renames
Phase 4 — Quick-start summaries (E)      ← polish, last
```
