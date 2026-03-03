---
term: idempotent reload
aliases:
  - full reload
  - config reload
domain: neovim configuration
tags:
  - reload
  - idempotency
---

Two capabilities, both required:

(A) Re-source config files without duplicating or accumulating state
(mappings overwrite, autocmds in cleared augroups, options idempotent).

(B) Add/remove plugins and fully reinitialize without restarting neovim.

Leaf plugin reload-safety is a separate concern — this definition covers
the config/framework layer only.
