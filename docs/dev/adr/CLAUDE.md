--- # workaround: anthropics/claude-code#13003
requires:
    - Skill(llm-collab)
---

# Architecture Decision Records

Significant decisions for this project. Also accessible via `decision-records.kb/`
symlink at repo root.

## What Belongs

A decision that constrains future work: choosing one option over alternatives,
establishing a policy, or ruling something out. Each ADR documents:

- **Status** — proposed, accepted, superseded, or rejected
- **Context** — the problem or question that forced a decision
- **Alternatives** — what was considered (including "do nothing")
- **Decision** — what was chosen
- **Rationale** — why, including tradeoffs accepted
- **Consequences** — what follows from this decision

## What Does NOT Belong

- Principles without alternatives (→ principles.kb/)
- Functional needs (→ needs.kb/)
- Implementation details (→ code)
- Session history (→ docs/dev/devlog/)

## Naming

`YYYY-MM-DD-NNN-slug.md` — date provides temporal ordering, NNN disambiguates
same-day decisions. When decisions conflict, newest wins.

## Creating ADRs

```bash
~/.claude/skills/llm-collab/bin/llm-collab-adr "Decision title"
```

## Superseding

When a new decision replaces an old one:
1. Create the new ADR referencing the old
2. Update the old ADR's status to "superseded by YYYY-MM-DD-NNN"
3. Do not delete the old ADR — the rationale history is valuable
