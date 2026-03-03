---
status: asserted
conclusion: claims.kb/two-tier-budgeted-testing.md
premises:
  - claims.kb/two-tiers-only.md
  - claims.kb/time-budgets-are-hard.md
  - claims.kb/capability-over-content.md
  - claims.kb/failure-driven-tests.md
  - claims.kb/test-profiles-not-permutations.md
tags:
  - testing
---

Maximizing invariant-value per second requires constraining tests on multiple
axes simultaneously: tier count (two), time budget (hard caps), test type
(capability not content), growth policy (failure-driven not proactive), and
scope (profiles not permutations). Each constraint independently prevents a
different mode of test suite entropy.
