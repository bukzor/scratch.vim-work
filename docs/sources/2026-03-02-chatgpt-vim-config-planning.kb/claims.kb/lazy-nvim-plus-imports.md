---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
tags:
  - distros
  - framework
  - architecture
---

Use lazy.nvim as foundation with custom profiles and a bespoke orchestrator.
Selectively import distro module specs (LazyVim Extras, AstroCommunity packs)
as supply, not as runtime framework. This maximizes durability and minimizes
framework lock-in while still benefiting from community-vetted module specs.
