---
status: asserted
conclusion: claims.kb/lazy-nvim-plus-imports.md
premises:
  - claims.kb/no-distro-as-runtime.md
  - claims.kb/distro-as-module-supply.md
  - claims.kb/distros-fight-reload.md
  - claims.kb/reload-contract.md
  - claims.kb/bespoke-orchestrator.md
tags:
  - distros
  - framework
---

No distro provides the full architecture needed, and distros actively fight
idempotent reload. But their module specs are valuable. A bespoke
orchestrator can enforce the reload contract that distros don't, while still
importing community modules. This separates module supply (distros are good
at this) from runtime framework (distros are bad at this for your goals).
