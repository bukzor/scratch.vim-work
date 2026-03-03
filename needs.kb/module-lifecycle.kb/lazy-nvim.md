# lazy.nvim — Module Lifecycle Capabilities

Source: ~/repo/github.com/folke/lazy.nvim/

## What it provides

### Plugin reload/teardown (not startup-only)

`Loader.deactivate(plugin)` (lua/lazy/core/loader.lua:202):
- Calls `mod.deactivate(plugin)` if the plugin's main module exports it
- Calls `plugin.deactivate(plugin)` if defined in spec
- Disables all lazy-loading handlers
- Clears lua module caches (`package.loaded`, `package.preload`)
- Clears `vim.g.loaded_*` flags
- Marks plugin as not loaded

`Loader.reload(plugin)` (lua/lazy/core/loader.lua):
- Calls deactivate
- Re-enables handlers
- Re-runs `plugin.init()`
- Re-loads if plugin was loaded or has startup events
- Re-sources vimscript files

### Config change detection (lua/lazy/manage/reloader.lua)

- 2-second polling timer watches all spec module files
- On change: reloads entire spec, fires `User LazyReload` event
- Configurable via `change_detection.notify`

### Conditional loading

Three mechanisms at different phases:

| Mechanism | Timing | Effect |
|-----------|--------|--------|
| `cond` | Parse-time | Skip plugin + dependents entirely |
| `enabled` | Parse-time | Disable plugin, keep for cleanup |
| `optional` | Parse-time | Remove if all fragments are optional |

All three work at both import level and plugin level. `cond` and `enabled`
accept booleans or functions.

### Spec merging

Fragment-based metatable chain. Multiple specs for the same plugin (identified
by name, url, or dir) are merged:
- `opts`, `dependencies`, `cmd`, `event`, `ft`, `keys` are always merged
- Other properties: last spec wins
- `opts_extend` allows deep-merging specific nested tables

### Lockfile (lua/lazy/manage/lock.lua)

`lazy-lock.json`: maps plugin name → `{ branch, commit }`.
- Written only by `:Lazy update`/`:Lazy sync`, not during startup
- Preserves entries for disabled plugins
- Sorted alphabetically (diff-friendly)
- Pure snapshot — doesn't affect loading logic directly

## What it does NOT provide

- **Namespace-based ownership** — no concept of "this augroup belongs to
  this module." Teardown clears lua caches but not vim-side state
  (augroups, user commands, keymaps) unless the plugin's own `deactivate()`
  handles it.
- **Deterministic teardown ordering** — `deactivate()` operates on one
  plugin at a time. No built-in "teardown all in reverse dependency order."
- **Profiles / feature flags** — no concept of named configurations or
  flag sets. Conditional loading via `cond`/`enabled` is per-plugin,
  not grouped.
- **Extra discovery** — no `has_extra()` equivalent. That's LazyVim-specific.

## Setup pipeline (for reference)

```
require("lazy").setup(spec, opts)
  → Config.setup()         -- merge options, reset rtp
  → Loader.setup()
    → Plugin.load()        -- parse specs → fragments → merged plugins
    → Handler.init()       -- register handler types
    → Handler.setup()      -- enable handlers for all plugins
  → Loader.startup()       -- load lazy=false plugins, run inits
  → User LazyDone event
```

## Key insight

lazy.nvim is NOT startup-only. The reload primitives exist and work.
The gap is in vim-side state management (namespaces) and higher-level
grouping (profiles/flags). A bespoke layer on top would be thin.
