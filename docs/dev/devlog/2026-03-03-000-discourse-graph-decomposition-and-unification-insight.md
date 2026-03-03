# Devlog: 2026-03-03 — Discourse graph decomposition and unification insight

## Focus

Used the `llm-discourse-graph` skill to decompose a ChatGPT vim config
planning conversation into a structured knowledge graph. The process
exposed design issues in the skill itself, leading to a proposal to unify
the discourse graph with the design knowledge tower.

## Session Progression

### Phase 1: Decomposition

Decomposed `docs/sources/2026-03-02-chatgpt-vim-config-planning.md` into
`docs/sources/2026-03-02-chatgpt-vim-config-planning.kb/`. Extracted
8 questions, 21 claims, 5 deductions, 1 definition, 1 source. Wired
everything via frontmatter cross-references.

### Phase 2: Schema fixes during use

Three schema gaps discovered:
- Questions needed `sources[]` (provenance)
- All node types needed `depends[]` (generic context reference)
- Schemas placed "at project root" was ambiguous — fixed to "alongside
  the collections they govern"

### Phase 3: Scoping refinement

Identified two questions as "strictly inner" to parent questions:
- `test-maintenance` inside `config-debug-hell`
- `reload-framework` inside `distro-alignment`

Moved them into `$ITEM.kb/` sub-scopes. Key heuristic discovered:
**move nodes down, don't reach in** — upward path resolution handles
outer references naturally, so explicit cross-scope paths are never needed
when the node lives in the right scope.

### Phase 4: Skill evaluation

Evaluated the completed graph for collaborative refinement/debate fitness.
Found three significant weaknesses:

1. All claims `status: asserted`, no `likelihood` — lost the ChatGPT
   confidence scores (0.78-0.85)
2. No structural distinction between observations and recommendations
3. Some claims too compound to contest individually

### Phase 5: Observation vs recommendation — the five-whys insight

Discussing whether to add a `kind` field to distinguish observations from
recommendations led to a key realization:

**The distinction isn't a type on the node, it's a position in the graph.**

- Walk `conclusion → premises` = asking "why?" (toward observations)
- Walk `premises → conclusion` = asking "how?" (toward prescriptions)

This is the five-whys/five-hows pattern. Claims near the leaves are
observations. Claims that are conclusions of deductions are prescriptive.
Adding a `kind` field would denormalize information already expressed by
the graph edges.

### Phase 6: Unification proposal

Recognized that the discourse graph and the design knowledge tower
(`how-to-document-design-knowledge.md` in llm-collab) express the same
relationship through different mechanisms:

| Feature | Design tower | Discourse graph |
|---|---|---|
| Why/how hierarchy | Numbered layers (010, 020...) | `$ITEM.kb/` nesting |
| Upward links | `why[]` | Deduction premises → conclusion |
| Abstraction visibility | Directory names | Must trace frontmatter |
| Epistemic tracking | None | `status`, `likelihood` |
| Open questions | None | `questions.kb/` |

**Rejected approach:** Keep both structures with a "promotion workflow"
(discourse graph conclusions graduate into design tower). Too complex,
duplicates work, un-parsimonious.

**Accepted direction:** Unify into one structure that gets benefits of both.

Key simplifications:
- Drop `deductions.kb/` — replace with `why[]` on claims. Reasoning lives
  in body text. Every deduction in the session was straightforward; the
  reified inference node added complexity without value.
- Nesting depth replaces numbered layers — outermost = highest abstraction,
  innermost = most concrete. Already demonstrated working.
- Flatten sub-scopes — no repeated collection directories inside `$ITEM.kb/`.
  Node type determined by frontmatter, not parent directory.
- Four collections: questions, claims, sources, definitions.

## Conventions Established

- **Interleave claims and deductions** (or claims and `why[]` wiring) —
  don't batch. Each claim is either justified or fundamental.
- **Source node first** when decomposing a document.
- **Move nodes down, don't reach in** for scoping decisions.
- **`todo.md` is a single prioritized list** — only `## Later` as section break.

## Open Questions

- Should `depends` and `why[]` coexist? Different semantics ("needs context"
  vs "exists because of") but two upward-linking fields adds complexity.
- How do mixed node types in a flat sub-scope work in practice? Does
  `questions.kb/mission.kb/goal-a.md` being a claim feel confusing?
- What replaces `kind: contradiction` deductions?

## References

- `docs/sources/2026-03-02-chatgpt-vim-config-planning.kb/` — the concrete instance
- `~/.claude/skills/llm-discourse-graph/SKILL.md` — skill updated during session
- `~/.claude/skills/llm-collab/references/how-to-document-design-knowledge.md` — the design tower
- `.claude/todo.kb/2026-03-03-000-unify-discourse-graph-and-design-tower-into-single-structure.md` — follow-up todo
