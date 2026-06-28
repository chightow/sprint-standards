---
name: sprint
description: Manages the sprint workflow for focused changes. Use when asked to add, fix, update, implement, debug, or build anything.
category: dev
tags: [workflow, planning, quality, tickets, orchestration]
---

# Sprint Workflow

CLI-backed commands:

| Command | When |
|---------|------|
| `sprint start` | Any normal or high-risk dev request |
| `sprint complete` | When you believe the work is done |

## Dispatch purposes

Tag every sub-agent dispatch in sprint flows with exactly one purpose:
- `implement` — build or modify the approved sprint scope.
- `review` — independently evaluate completed work, risks, or acceptance evidence.
- `explore` — read and map a subsystem before implementation decisions.

## Workflow tiers

### Trivial
Use no sprint when: question/explanation, single-line change, user explicitly says to skip. Work directly, report verification.

### Normal
Default for focused, reversible changes. Run `sprint start`, create acceptance criteria, build after approval.

### High-risk
Use full pipeline when: security-sensitive, irreversible, broad blast radius, multiple trigger paths, gray areas. High-risk sprints run orient, impact analysis, required mitigation tests, and full wrapup.

## Files

```
.tickets/<id>/
  ticket.md        ← YAML frontmatter + body; never edit status directly
  acceptance.md    ← definition of done + test plan
  plan.md          ← approach, decisions; sign-off block
  research.md      ← optional; high-risk/brownfield only
  eval-report.md   ← adversarial criterion grades with verdict
```

## Close gates

`sprint complete` blocks if:
- Non-trivial tickets aren't closed/cancelled/archived
- `eval-report.md` is missing (unless `tier: trivial` in plan.md frontmatter)
- `evaluator-run-id` doesn't match a subagent-runs.jsonl entry
- Verdict isn't `pass:`
