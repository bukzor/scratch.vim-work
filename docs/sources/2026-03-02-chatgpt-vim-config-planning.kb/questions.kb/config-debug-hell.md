---
sources:
  - sources.kb/chatgpt-vim-config-planning.md
depends:
  - questions.kb/neovim-choices.md
candidate-resolutions:
  - claims.kb/containment-over-testing.md
tags:
  - config-entropy
  - testing
  - debugging
---

How do you keep a fancy neovim config without it becoming un-debuggable?
Is regression testing the answer, or does that create its own maintenance hell?

Context: months of "good ideas" accumulate, plugin interactions cause failures
that are hard to isolate without causing further problems.
