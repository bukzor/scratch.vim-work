# LazyVim Extras — Module Lifecycle Layer

Source: ~/repo/github.com/LazyVim/LazyVim/

LazyVim builds a "feature flag" system on top of lazy.nvim's import mechanism.
This documents what it provides and where it's coupled to the LazyVim framework.

## What it provides

### Extras as feature packs

Each extra is a lua file returning lazy.nvim plugin specs. Organized by category:
lang.*, editor.*, coding.*, ui.*, dap.*, ai.*, formatting.*, linting.*, test.*, util.*

Enabling an extra adds its specs to the plugin loading pipeline via lazy.nvim's
`{ import = "module.path" }` mechanism.

### State persistence (lazyvim.json)

```json
{
  "version": 8,
  "extras": [
    "lazyvim.plugins.extras.lang.typescript",
    "lazyvim.plugins.extras.editor.fzf"
  ]
}
```

Edited via `:LazyExtras` UI or manually. Changes require restart.

### has_extra() discovery

Checks three sources:
1. Already-imported modules in lazy.nvim's spec.modules
2. Entries in lazyvim.json extras array
3. Manual imports in lazy.nvim's options.spec

Allows conditional config: `if LazyVim.has_extra("lang.rust") then ... end`

### Mutual exclusion groups

Three groups where only one option should be active:
- **picker**: snacks_picker / fzf / telescope
- **cmp**: blink / nvim-cmp
- **explorer**: snacks_explorer / neo-tree

Resolution: global variable override → already-enabled extra → first in list.
The losing options get `enabled = false` in their specs.

### Priority-based loading (xtras.lua)

Extras are sorted by priority before importing:
- Priority 1: test.core, dap.core
- Priority 2: nvim-cmp, neo-tree (legacy defaults)
- Priority 20: auto-enabled defaults
- Priority 50: everything else (default)

### Extra metadata

Extras can export a `recommended` field — a function or table that tells
`:LazyExtras` whether to suggest enabling it (e.g. "you have Rust files,
consider enabling lang.rust").

## What's tightly coupled to LazyVim

- `LazyVim.has_extra()` — uses LazyVim's own config and json modules
- `LazyVim.pick.register()` — framework's picker abstraction
- `LazyVim.config.get_defaults()` — mutual exclusion logic references
  LazyVim's internal config state
- Module paths are hardcoded to `lazyvim.plugins.extras.*`
- Import order validation assumes LazyVim's 3-stage structure
  (core → extras → user)
- `recommended` metadata evaluated by LazyVim-specific UI code

## What's a general pattern (reusable as a design)

- JSON manifest of enabled features — trivially reimplementable
- Categorized extras directories — just a file organization convention
- Mutual exclusion groups — ~30 lines of logic, independent of framework
- Priority-based import ordering — ~20 lines of sorting
- `has_extra()` concept — ~15 lines if built on lazy.nvim directly

## Estimated cost to reimplement the useful parts

The general patterns total ~80-100 lines of lua. The LazyVim-specific coupling
(picker registration, recommendation UI, import order validation) is another
~200 lines we'd skip.

A bespoke "extras-like" system on bare lazy.nvim would need:
- A JSON or lua config file listing enabled features (~20 lines)
- A loader that converts features to lazy.nvim import specs (~30 lines)
- A has_feature() query function (~15 lines)
- Mutual exclusion enforcement (~30 lines)
- Profile presets mapping profile name → feature set (~10 lines)
