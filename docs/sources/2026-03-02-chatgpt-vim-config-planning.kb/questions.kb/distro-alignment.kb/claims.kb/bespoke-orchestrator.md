---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
depends:
  - definitions.kb/idempotent-reload.md
tags:
  - framework
  - reload
  - architecture
---

A thin bespoke orchestrator over lazy.nvim (module registry with
setup/teardown/depends, ownership namespaces, reload_all and
reload_module primitives) best enforces the reload contract and makes
reload the default path rather than an afterthought.
