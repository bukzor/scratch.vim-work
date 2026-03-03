--- # workaround: anthropics/claude-code#13003
depends:
    - skills/llm-collab
    - skills/llm-subtask
requires:
    - Skill(llm.kb)
---

# scratch.vim - Vim Config Modernization

Scratch space for planning and implementing a comprehensive overhaul of bukzor's vim configuration (~18 years of accumulated config, using vim since 2008).

## Current Work

Check `.claude/todo.md` and `.claude/todo.kb/` for active efforts. Load `Skill("llm-subtask")` for maintenance.

## Context

This is a planning/scratch repo, not the live vim config itself. We use this space to:
- Audit the existing config and identify pain points
- Research modern vim/neovim ecosystem options
- Prototype and test configuration changes
- Plan a migration path

## Knowledge Base

- `decisions.kb/` — Layered decision knowledge (facts → values → principles → choices)
- `needs.kb/` — Functional needs + evaluated options per need
- `questions.kb/` — Open questions awaiting resolution
- `stack.kb/` — Symlinks to chosen options (the adopted config)

## Conventions

- Session history goes in `docs/dev/devlog/`
- ADRs go in `docs/dev/adr/` (process/methodology decisions)
- Active tasks in `.claude/todo.md`
