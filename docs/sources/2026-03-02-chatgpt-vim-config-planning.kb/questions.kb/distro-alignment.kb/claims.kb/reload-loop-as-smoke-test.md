---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
depends:
  - claims.kb/reload-contract.md
  - claims.kb/two-tier-budgeted-testing.md
tags:
  - testing
  - reload
---

Running ReloadAll twice in a row and asserting no errors is an extremely
high invariant-value-per-second smoke test. It catches state accumulation
(the main reload failure mode) cheaply. Similarly, ReloadModule on a
single module run twice catches per-module teardown bugs.
