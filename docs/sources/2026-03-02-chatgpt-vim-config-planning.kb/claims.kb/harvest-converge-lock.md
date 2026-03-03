---
status: asserted
sources:
  - sources.kb/chatgpt-vim-config-planning.md
tags:
  - migration
---

Unifying divergent config branches should follow harvest → converge → lock:
extract candidates from all branches into a prioritized list (with Why, Tier,
Proof per item), build a fresh tiered skeleton, migrate items by tier, add
minimal tests, then freeze and prune. Don't merge git histories — copy
deliberately into the new structure.
