# Testing Strategy: Two Tiers with Hard Budgets

**Status:** accepted

## Context

Fancy vim configs become un-debuggable when plugin interactions accumulate
silently. Full regression testing of a vim config is its own maintenance burden.
We need high "invariant-assertion-value per second" with low activation energy
for adding tests.

## Alternatives

1. **No tests** — rely on manual verification. Fast initially, but breakage
   compounds over time.

2. **Comprehensive test suite** — test every plugin, keymap, and behavior.
   High coverage but becomes a second project to maintain.

3. **Two-tier capability tests with hard time budgets** — smoke (≤3s) and
   scenario (≤20s), capability-focused, failure-driven additions only.

## Decision

Option 3: two tiers with strict budgets.

## Rationale

- Capability tests ("is LSP alive?") survive refactors; content tests
  ("is inlay hint format X?") rot
- Hard time budgets prevent test suite entropy — if a test is slow, it gets
  deleted or demoted, not tolerated
- Failure-driven additions (1 new test per painful incident) ensure every
  test has proven value
- Profile-based matrix (test survival/core/full, not every plugin permutation)
  keeps combinatorics bounded

## Design

**Smoke (always run, ≤3s total):**
- Survival-mode vim boots without errors
- Neovim core profile boots without errors
- Neovim full profile boots without errors
- ReloadAll completes without errors
- ReloadAll twice catches state accumulation

**Scenario (upgrade day, ≤20s total):**
- Telescope opens and returns entries
- Completion produces ≥1 item
- LSP attaches to a fixture file
- (Optional) DAP starts and hits breakpoint

## Consequences

- Need a fixture directory (tiny Rust file, tiny Lua file)
- Need a small helper API: boot(profile), open_fixture, wait_for_lsp, assert_no_errors
- Need a single command to run smoke suite
- Tests are added reactively, not proactively
