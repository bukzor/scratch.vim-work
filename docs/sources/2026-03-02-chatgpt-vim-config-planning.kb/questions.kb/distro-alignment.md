---
sources:
  - sources.kb/chatgpt-vim-config-planning.md
depends:
  - questions.kb/unify-branches.md
candidate-resolutions:
  - claims.kb/lazy-nvim-plus-imports.md
tags:
  - neovim
  - distros
  - modularity
---

Do any neovim distros (LazyVim, AstroNvim, LunarVim, etc.) align with
the goals of tiered profiles, survival-mode portability, smoke testing,
and incremental migration? Do their module systems provide useful things
I'd otherwise have to invent, or am I better off bespoke?

Additional constraints:
- Configs must be loadable/reloadable idempotently.
- If using a distro, it would be in opt-in mode only loading things actively wanted.
- Survival-kit vim configs layered underneath.
