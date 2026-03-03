---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
tags:
  - profiles
  - debugging
---

If the config can run in "core-only" and "full" modes via a single switch,
the first debugging question becomes "does it break in core or only full?"
— instant narrowing. With modular plugin buckets, bisection reduces a
many-plugin interaction bug to a small culprit set in minutes.
