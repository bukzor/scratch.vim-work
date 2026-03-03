---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
tags:
  - testing
---

Hard suite time limits prevent test suite entropy. Smoke ≤3s, scenario ≤20s,
any single test ≤2s. If a test exceeds budget, it gets deleted, moved to
scenario, or rewritten.
