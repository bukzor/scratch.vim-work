# Decisions

Layered decision knowledge, ordered from most fundamental to most concrete.

## Collections

- `000-raw-facts.kb/` — Empirical observations: what is true about the world
- `005-constitutional-values.kb/` — Commitments: what we value given those facts
- `010-design-principles.kb/` — Derived principles: how to act given those values
- `050-technical-decisions.kb/` — Concrete choices: what to build given those principles

Higher-numbered collections depend on lower-numbered ones. Each item should
trace back to its predecessors via "Derives from:" or "Follows from:" lines.

## Primary Source

`docs/sources/2026-03-02-chatgpt-vim-config-planning.md` — the exploratory
conversation that produced these decisions. Read it to check for uncaptured
reasoning or to mine further.
