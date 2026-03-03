---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
depends:
  - definitions.kb/idempotent-reload.md
tags:
  - reload
  - framework
---

Idempotent reload requires an explicit lifecycle contract: setup() is
idempotent, optional teardown() clears side effects, no implicit global
side effects at require-time, and all side effects are discoverable and
removable (augroups, user commands, keymaps, highlight groups, plugin
globals — each with ownership namespaces).
