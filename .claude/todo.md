---
managed-by: Skill(llm-subtask)
cost-benefit-sweh:
  timebox:
    "@value": 6.0
    rationale: |
      Parent index. Child unify-discourse-graph (8h) rated separately.
      Residual: gather/audit existing vim config (~1.5h), identify
      pain points / past sins (~1h), survey modern vim/neovim
      ecosystem (~2h), define goals/non-goals (~1h), plus the Later
      items (design target arch, plan migration path).
    confidence: tentative
  benefit-2w:
    "@value": 0.5
    rationale: |
      Discovery/scoping phase — outputs feed downstream config
      modernization. Modest in-window value; bigger downstream.
    confidence: tentative
  cost-of-delay-2w:
    "@value": 0.1
    rationale: |
      Personal tooling, exploratory. Current vim config works;
      delay cost is only context decay on the modernization plan.
    confidence: tentative
---

- [~] .claude/todo.kb/2026-03-03-000-unify-discourse-graph-and-design-tower-into-single-structure.md
- [ ] Gather and audit existing vim configuration
- [ ] Identify pain points and "past sins" to address
- [ ] Survey modern vim/neovim ecosystem and best practices
- [ ] Define goals and non-goals for the modernized config

## Later

- [ ] Design target configuration architecture
- [ ] Plan migration path from current to target
