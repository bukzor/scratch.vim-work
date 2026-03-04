subtask load

Close all lanes. The unified claim scheme design is resolved — now
implement it and converge back to vim config work.

## Lanes to Close

### Lane C: Unified Claim Scheme (skill work)

Design resolved 2026-03-04. Parentage generalized from why/how to
question/answer. See devlog: `bukzor-agent-skills/llm-discourse-graph/
docs/dev/devlog/2026-03-04-000-lane-mixing-resolution-and-question-answer-generalization.md`

Remaining implementation:
1. Write JSON Schema for unified claim format (validity-axes $defs drafted in spec)
2. Update SKILL.md for unified structure
3. Update how-to-document-design-knowledge.md in llm-collab

### Lane B: Discourse Graph Extraction (proving ground)

4. Migrate chatgpt-vim-config-planning.kb to unified format (first real test)
5. Apply to user preferences (second test, staged at `~/.claude/user-preferences.kb/`)

### Lane A: Vim Config Modernization (the actual goal)

6. Reconcile decisions.kb/ with unified discourse graph
7. Resume vim config work — the knowledge base should now be usable

## Early Decisions (discuss with user)

- **Push "directories=questions" down to llm.kb?** The structural
  semantics (directories SHALL be questions, files are answers) fit
  llm.kb, not discourse-graph. Discourse graph would inherit and add
  epistemic machinery (validity, per-party, sources, why[]).
- **Extract llm-design-doc skill?** The design tower pattern
  (how-to-document-design-knowledge.md) is currently buried in
  llm-collab's references. It's really "llm.kb where all questions
  are how?" — a skill, not a reference doc. This gives a clean stack:
  ```
  llm.kb              — filesystem pattern, directories=questions
  llm-design-doc      — llm.kb + all questions are "how?" + tower
  llm-discourse-graph — llm.kb + validity + per-party + sources
  ```
  llm-collab then owns workflows (devlogs, ADRs, sessions), not
  data structures.

## Constraints

- **Design = discuss with user.** Open questions remain (see spec).
  Propose and discuss before resolving them.
- **One small step at a time.** The migration (step 4) is the first real
  validation of the unified scheme. Expect to discover issues.
- **Lane C serves Lane A.** Don't gold-plate the skill — get it working
  well enough to unblock vim config, then iterate.

## Before Starting

1. Read the living spec: `~/.claude/skills/llm-discourse-graph/docs/dev/design/unified-claim-scheme.md`
2. Read the latest devlog (2026-03-04-000)
3. Check todo.kb/ for any updates
