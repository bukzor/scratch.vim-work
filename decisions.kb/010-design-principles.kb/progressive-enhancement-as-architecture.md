# Progressive Enhancement as Architecture

Environments vary in hostility: bare vi on a k8s pod, neovim over ssh, neovim
on a local workstation with full plugins. The config should degrade gracefully
across this spectrum, not break at the first missing dependency.

This means tiered profiles are not just a convenience — they're the
architectural expression of portability. Each tier assumes only what its
target environment guarantees:

- Tier 0 (survival): system vi/vim, no plugins, no assumptions
- Tier 1 (core): neovim available, core plugins, no network/GUI assumed
- Tier 2 (full): local workstation, all plugins, luxury features

Features detect their prerequisites and fail soft. No tier requires a
higher tier to be present.

Derives from: diverse-environments, transferrable-leaf-configs
