---
name: skill-setup-std
description: Validates skill files against canon standards. Use when adding a new skill or auditing existing ones.
category: agent-ops
tags: [skills, contributors, conventions]
version: 1.8.0
updated: 2026-06-17
---

# Skill Setup Standard

Rules for adding or modifying skills. Follow these so every skill behaves predictably.

## File Location

Skills follow a two-tier layout:
- **Standalone skills**: `skills/<name>/SKILL.md`
- **Hidden/internal skills**: `skills/<name>/SKILL.md` with `hidden: true` frontmatter

## Naming

- Lowercase, hyphenated directory name: `skills/sprint/`, `skills/context-check/`
- Prefer gerund form (verb + -ing): `processing-pdfs`, `analyzing-spreadsheets`
- The skill file is always named `SKILL.md`

## Frontmatter

Every skill requires these fields:

```yaml
---
name: my-skill
description: One sentence — what it does and when to use it.
category: dev | agent-ops | ops
tags: [tag1, tag2]
---
```

Write descriptions for models, not just humans. Always use third person. Include what it does AND when to use it. Description + when_to_use capped at 1,536 characters.

Optional fields: `when_to_use`, `argument-hint`, `arguments`, `disable-model-invocation`, `user-invocable`, `allowed-tools`, `disallowed-tools`, `model`, `effort`, `context: fork`, `agent`, `hooks`, `paths`, `shell`, `summary`, `depends`, `hidden`.

## One job

A skill that does two things is two skills waiting to be separated. If you find yourself writing "and then" in the description, split it.

## Minimal content

State the job, the steps, and the stop condition. Cut everything else. Hard limit: 500 lines for SKILL.md body.

## Progressive disclosure

SKILL.md is a table of contents, not an encyclopedia. Split content into reference files. Keep references one level deep from SKILL.md. Reference files longer than 100 lines need a table of contents.

## Gotchas

Add a `## Gotchas` section to any skill where real usage has revealed failure patterns. One bullet per gotcha, led by the condition and what to do instead.

## Testing

Build evals before extensive documentation. Three scenarios minimum in `skills/<name>/evals/evals.json`. Cover at least three of: control, edge, compliance, boundary, over-caution.
