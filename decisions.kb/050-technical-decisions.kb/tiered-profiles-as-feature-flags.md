# Tiered Profiles as Feature Flags

Config capabilities are controlled by feature flags. Profiles are named presets
of flags, ordered as supersets:

- **Tier 0 (survival):** no flags — pure vim baseline, no plugins, no framework
- **Tier 1 (core):** flags for daily-driver essentials (LSP, completion, navigation)
- **Tier 2 (full):** core flags + luxury features (UI candy, debugging, extras)

Each individual capability is a flag, not a hardcoded piece of a profile.
Profiles just select which flags are on by default.

## Novel features start default-off

New or experimental capabilities are added as flags outside any profile. To
use them, you opt in explicitly. Once a feature has proven its value through
actual use, it gets promoted into the appropriate profile tier.

This is the concrete mechanism for demand-driven curation: the flag exists,
but earns its profile membership by being missed when absent.

## Bisection via flags

When something breaks, toggle flags to isolate the problem. A modular flag
system makes this minutes, not hours. The flag granularity determines the
bisection resolution.

## Transferrability via flags

A self-contained feature flag — one that works independently — is a
transferrable unit. "Grab this flag file" becomes the mentoring use case.

Follows from: progressive-enhancement-as-architecture, demand-driven-curation,
containment-over-testing, transferrable-leaf-configs
