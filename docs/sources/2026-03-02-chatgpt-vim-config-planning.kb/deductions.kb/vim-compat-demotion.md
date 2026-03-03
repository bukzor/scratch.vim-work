---
status: asserted
conclusion: claims.kb/demote-vim-compat.md
premises:
  - claims.kb/vim-compat-only-if-exercised.md
  - claims.kb/entropy-not-portability.md
  - claims.kb/survival-kit-preserves-portability.md
  - claims.kb/portability-is-behavioral.md
  - claims.kb/tiered-hostility.md
  - claims.kb/demand-driven-curation.md
tags:
  - vim-compat
  - portability
---

If vim-compat is only valuable when exercised, and the real pain is config
entropy not portability, then full vim-compat is a tax. A small survival kit
captures the actual portability benefit. Behavioral portability (tiered
profiles, fail-soft enhancement) replaces language-level compatibility as
the architectural constraint. Legacy config gets demand-driven curation
instead of unbounded preservation.
