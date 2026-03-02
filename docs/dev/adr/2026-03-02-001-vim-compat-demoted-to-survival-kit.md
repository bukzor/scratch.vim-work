# Vim Compatibility Demoted to Survival Kit

**Status:** accepted

## Context

The existing config (dating from 2008) treats vim-compatibility as a blanket
constraint: everything must work in plain vim. This served portability across
macOS, Windows, headless k8s, ssh+tmux Linux, etc.

Over time this constraint accumulated sediment — years of vimrc.d/*.vim files
with defaults, nitpick fixes, finger savers, and typo correctors. The
compatibility guarantee was rarely exercised but constantly taxed the config's
architecture.

## Alternatives

1. **Full vim-compat as constitutional** — everything works in vim and neovim.
   Preserves maximum portability but constrains modernization and accumulates
   entropy indefinitely.

2. **Drop vim-compat entirely** — go neovim-only. Simplest path forward but
   loses the ability to function in minimal environments.

3. **Small vim survival kit + neovim-native primary** — keep a capped,
   portable vim baseline; make neovim the primary config target.

## Decision

Option 3: demote full vim-compat to legacy; promote a small survival kit to
constitutional status.

## Rationale

- Portability is the real value, not vim-compatibility per se
- A capped survival kit (~300 lines) preserves portability without constraining
  the neovim config's architecture
- "Demand-driven curation" — start clean, graduate only what you miss — prevents
  unbounded legacy accumulation
- The survival kit can be smoke-tested independently

## Consequences

- Need to define what goes in the survival kit (sensible defaults, core keymaps,
  terminal safety — no plugins, no cleverness)
- Existing vimrc.d/ becomes a "fossil record" to mine, not a living config
- Neovim config is free to use lua, treesitter, LSP, and other nvim-only features
