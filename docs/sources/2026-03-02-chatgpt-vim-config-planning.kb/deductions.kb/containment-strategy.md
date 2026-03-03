---
status: asserted
conclusion: claims.kb/containment-over-testing.md
premises:
  - claims.kb/config-entropy-compounds.md
  - claims.kb/pinning-makes-breakage-intentional.md
  - claims.kb/profiles-enable-bisection.md
  - claims.kb/smoke-tests-not-a-project.md
tags:
  - debugging
  - config-entropy
---

If config entropy compounds through plugin interactions and unpinned updates,
then the leverage points are: making breakage intentional (pinning), making
failure isolation fast (profiles + bisection), and catching gross breakage
cheaply (smoke tests). Full regression testing addresses none of these
directly and adds its own maintenance surface.
