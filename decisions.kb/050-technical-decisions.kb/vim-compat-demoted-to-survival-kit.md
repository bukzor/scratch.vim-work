# Vim Compat Demoted to Survival Kit

Full vim-compatibility is no longer a blanket constraint. Instead: a small,
capped vim survival kit (~300 lines) provides portability where neovim isn't
available, and the primary config targets neovim natively.

The survival kit contains: sensible defaults, core keymaps, terminal safety.
No plugins, no plugin manager, no cleverness. If it can't fit in the cap, it
isn't survival-kit material.

The existing vimrc.d/ becomes a fossil record to mine on demand — not loaded
by default. Items graduate into the survival kit or neovim config only when
actively missed.

Follows from: portability-not-vim-compat, containment-over-testing
