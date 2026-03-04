---
anthropic-skill-ownership: llm-subtask
---

# Unify discourse graph and design tower into single structure

**Priority:** High
**Complexity:** High
**Context:** `docs/dev/devlog/2026-03-03-000-discourse-graph-decomposition-and-unification-insight.md`

## Motivation

This isn't just infrastructure for the vim config. The unified structure
is a reusable tool for a recurring problem: extracting actionable knowledge
from LLM conversations. There are ~20 past discussions across chatgpt.com
and claude.ai that would become actionable given similar treatment. The vim
config conversation is the proving ground; the skill is the real deliverable.

## Problem Statement

Two knowledge structures serve overlapping purposes:
- `llm-discourse-graph` skill: questions, claims, deductions, sources, definitions
- `how-to-document-design-knowledge` (in llm-collab): mission → goals → requirements → design → components → deliverables

Both use `llm.kb` pattern, both organize knowledge hierarchically, both use
YAML frontmatter cross-references. But they don't interoperate and work gets
duplicated (e.g. `decisions.kb/` and the discourse graph contain the same
conclusions from the same source).

## Key Insight from Session

The five-whys/five-hows tower and the discourse graph express the same
relationship: "why does this exist?" (walk up) / "how is this realized?"
(walk down). The design tower uses numbered layers (010, 020...) to make
abstraction visible. The discourse graph uses `$ITEM.kb/` nesting.

Nesting depth CAN replace numbered layers: outermost = highest abstraction,
innermost = most concrete. We demonstrated this with
`config-debug-hell.kb/test-maintenance` (parent = why, child = how).

## Proposed Unified Structure

### Four collections, not five

Drop `deductions.kb/`. Add `why[]` to claims. Reasoning lives in body text.

- `questions.kb/` — open inquiries
- `claims.kb/` — assertions with `status`, `likelihood`, `why[]`
- `sources.kb/` — provenance
- `definitions.kb/` — terminology

### Nesting replaces numbered layers

Top-level collections are entry points. Sub-scopes use `$ITEM.kb/` only —
no repeated collection directories inside.

```
questions.kb/
  config-debug-hell.md
  config-debug-hell.kb/
    test-maintenance.md        ← type from frontmatter, not directory
    two-tiers-only.md
    capability-over-content.md
```

NOT:
```
questions.kb/
  config-debug-hell.kb/
    questions.kb/              ← redundant
      test-maintenance.md
    claims.kb/                 ← redundant
      two-tiers-only.md
```

Depth = abstraction level. Walk down for "how", walk up for "why".

### `why[]` replaces deductions for simple cases

A claim with `why: [claims.kb/a.md, claims.kb/b.md]` says "I hold because
of these." Body text explains the inference. Same as design tower's `why[]`.

Deductions were useful when the inference itself was contestable. In
practice during the session, every deduction was straightforward. The body
text of the conclusion claim can carry the reasoning.

### Epistemic metadata everywhere

`status: asserted|contested|retracted` and `likelihood: 0-1` apply to any
node. This is what the discourse graph adds beyond the design tower.

### Node type from frontmatter, not directory

Inside a sub-scope, how do you distinguish a question from a claim?
By its frontmatter schema:
- Questions have `candidate-resolutions` or `resolved`
- Claims have `status`, `why[]`
- Sources have `kind`, `title`
- Definitions have `term`

Top-level collection directories still serve as typed entry points.

## Implementation Steps

Design spec drafted at `llm-discourse-graph/docs/dev/design/unified-claim-scheme.md`
with component discussions in `unified-claim-scheme/`. The redesign went
further than originally planned — one node type, three validity axes,
per-party override via merge-patch.

- [x] Design the unified schema set
    - [x] One node type (claim) replaces five collections
    - [x] Validity axes (truth, certainty, utility) replace status/likelihood
    - [x] Per-party validity with $all and RFC 7396 merge-patch semantics
    - [x] Source attribution as claim metadata, not a collection type
    - [x] Parentage-as-why/how replaces numbered layers and deductions
- [ ] Write JSON Schema for the unified claim format
    - [ ] validity-axes and validity $defs (drafted in spec)
    - [ ] Full claim schema (why[], sources, validity, resolved, etc.)
- [ ] Update SKILL.md for the unified structure
- [ ] Apply to user preferences (first test case)
    - [ ] Analyze three preference docs using unified scheme
    - [ ] Source files staged at `~/.claude/user-preferences.kb/`
- [ ] Migrate chatgpt-vim-config-planning.kb to unified format
- [ ] Reconcile with decisions.kb/ in scratch.vim-work
- [ ] Update how-to-document-design-knowledge.md in llm-collab

## Open Questions

- Should `why[]` be conjunctive (default) or allow disjunctive support?
- How to express contradiction without negation claims? (positive-only, watch item)
- How to contest reasoning specifically vs the conclusion? (meta-claims, watch item)
- Should design tower layer names survive as a naming convention?
- Inline/short vs file-based/long claim format — want a lightweight tier?
- Fate of `depends` alongside `why[]` — still unresolved

## What Worked in the Session (preserve these)

- `$ITEM.kb/` nesting for why/how hierarchy
- Upward path resolution (inner scopes reference outer without explicit paths)
- "Move nodes down, don't reach in" as the scoping heuristic
- Interleaved claim+deduction creation (becomes: interleaved claim+why wiring)
- Source node first, questions second, claims third
- Epistemic metadata catching confidence levels from source material

## What Didn't Work (fix these)

- Flat claims.kb/ with 19 claims — no visible hierarchy
- Deductions as separate nodes — added complexity without much value
- `candidate-resolutions` pointing to deductions (schema said claims)
- Repeated `questions.kb/` inside sub-scopes
- Missing `likelihood` values despite source having confidence scores
