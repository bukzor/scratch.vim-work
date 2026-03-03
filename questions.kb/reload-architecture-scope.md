# How much reload infrastructure do we build vs reuse?

## Context

We originally decided on a bespoke orchestrator (~100-200 lines) to handle
module lifecycle: register/setup/teardown, namespace management, deterministic
ordering. This assumed lazy.nvim was startup-only.

Research revealed lazy.nvim already has substantial reload support:
- `Loader.deactivate()` — clears lua modules, calls `deactivate()` hook,
  disables handlers, clears `vim.g.loaded_*` flags
- `Loader.reload()` — deactivate + re-enable handlers + re-run init + re-load
- Config change watcher (2-second polling, auto-reloads specs)
- `cond`, `enabled`, `optional` at both import and plugin level

See: needs.kb/module-lifecycle.kb/lazy-nvim.md for full findings.

## What's still needed (not in lazy.nvim)

- Namespace-based ownership (augroups, user commands, keymaps per module)
- Deterministic teardown ordering (reverse dependency order)
- "Profiles" as named feature-flag sets
- `has_extra()`-style queries for conditional config

## The question

How much of LazyVim's extras layer (xtras.lua + has_extra() + mutual exclusion
+ lazyvim.json state) is worth adopting vs reimplementing on bare lazy.nvim?

Options range from:
1. Pure lazy.nvim + tiny glue (~50 lines for namespaces + profiles)
2. Vendor/adapt LazyVim's extras layer (~300 lines, tightly coupled)
3. Adopt LazyVim as runtime after all (reverses no-distro-as-runtime decision)

## What would resolve this

Prototyping. Build a minimal profile system on bare lazy.nvim and see if it
covers the use cases. If we keep wanting LazyVim's extras features, option 2
or 3 becomes more compelling.

## History

Originally captured as a technical decision ("bespoke orchestrator"), demoted
to open question after discovering lazy.nvim's existing reload support.
