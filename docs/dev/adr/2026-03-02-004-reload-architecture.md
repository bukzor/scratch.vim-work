# Reload Architecture: Bespoke Orchestrator with Lifecycle Contract

**Status:** accepted

## Context

Idempotent config reload (both full and per-module) without restarting neovim is
a constitutional requirement. This enables "just-in-time" config changes and
eliminates the restart tax during development.

Many lua plugins don't support reload. We accept that and either fix them, wrap
them, or drop them. The constraint is: the *framework* must not be the obstacle.

## Alternatives

1. **Accept restart as the reload mechanism** — simplest, but loses the
   ability to iterate on config without losing editor state.

2. **Use a distro's reload support** — lazy.nvim has `:Lazy reload` but
   plugins aren't guaranteed reload-safe; distros add their own state.

3. **Bespoke orchestrator with explicit lifecycle contract** — every module
   registers setup/teardown; framework manages namespaces and ordering.

## Decision

Option 3: bespoke orchestrator.

## Rationale

- The reload contract (setup is idempotent, teardown clears side effects, no
  require-time side effects) is simple to state and enforce
- Namespace-based ownership (augroups, commands, keymaps per module) makes
  teardown trivial and reliable
- A module registry gives deterministic ordering and reverse-order teardown
- This is the single most leverageful piece of infrastructure to build

## Design

**Module contract:**
- `register(name, { setup, teardown, depends })`
- `setup()` is idempotent — safe to run twice
- `teardown()` clears all side effects (optional but encouraged)
- No side effects at require-time — only inside setup()

**Namespace conventions:**
- Augroups: `User::{module}`
- User commands: `User{Module}*`
- Keymaps: tracked per-owner for clean removal

**Orchestrator primitives:**
- `runtime.reload_all()` — teardown reverse, clear caches, setup forward
- `runtime.reload(name)` — teardown/setup one module + dependents

**Standard teardown helpers:**
- `clear_augroup(name)`
- `del_user_commands_prefix(prefix)`
- `unmap_owner(name)`

## Consequences

- Every module must comply with the contract (enforcement via convention +
  smoke tests that run reload twice)
- Leaf plugins that aren't reload-safe need wrappers or replacement
- The orchestrator itself is small (~100-200 lines) but critical path
- Reload loops become high-value smoke tests
