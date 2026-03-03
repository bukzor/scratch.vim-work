---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
tags:
  - portability
  - architecture
---

Portability should be a behavioral guarantee (fail-soft progressive
enhancement, dependency-free baseline), not a language/compatibility
constraint. The purpose is surviving diverse environments; Vimscript
is only one way to achieve that and pushes toward monolithic codepaths
that accumulate sediment.
