# Testing: Two Tiers with Hard Budgets

Two test tiers only. Hard time budgets enforced mechanically.

**Smoke (always run, ≤3s total):** proves the config boots and core plumbing
responds. Survival vim boots. Neovim core boots. Neovim full boots. ReloadAll
completes. ReloadAll twice doesn't accumulate state.

**Scenario (upgrade day, ≤20s total):** proves real workflows work. Telescope
opens. Completion produces items. LSP attaches.

Tests are capability-focused ("is it alive?"), not content-focused ("is it
formatted how I like?"). New tests are added only after a painful regression —
one test per incident, max. Any test exceeding budget gets deleted or rewritten,
not tolerated.

Profiles are the test matrix, not plugin combinations.

Follows from: containment-over-testing, invest-for-durability
