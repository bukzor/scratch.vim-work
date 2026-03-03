---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
depends:
  - definitions.kb/idempotent-reload.md
tags:
  - distros
  - reload
---

Distros add framework-level state, implicit side effects, and load-order
magic not designed around teardown/re-init. Implicit module execution on
require(), caching, one-time init hooks, unclear ownership of augroups/keymaps,
and non-invertible config merging all make idempotent reload harder.
