# No Distro as Runtime Framework

**Status:** accepted

## Context

Neovim "distros" (LazyVim, AstroNvim, LunarVim, NvChad) offer opinionated
defaults, modular plugin management, and curated integrations. They could
accelerate initial setup.

However, we require idempotent full-config reload without restart, per-module
reload, and strict tiered profiles (survival/core/full). These are constitutional
requirements.

## Alternatives

1. **Adopt a distro as the runtime** — use LazyVim or AstroNvim as the base
   framework, customize on top.

2. **Bespoke framework on lazy.nvim** — build a thin orchestrator with module
   registry and lifecycle contract; import distro modules selectively.

3. **Fully bespoke** — no external plugin manager, hand-roll everything.

## Decision

Option 2: bespoke thin framework on lazy.nvim, with distro ecosystems as
module supply chains.

## Rationale

- Distros optimize for "install once, live inside it" — they add implicit state,
  load-order magic, and startup-only lifecycle assumptions that fight reload
- LazyVim Extras and AstroCommunity are valuable module libraries, but their
  value is in the specs, not the runtime
- lazy.nvim alone provides the plugin loading primitives we need
- A bespoke orchestrator can enforce the reload contract at the framework boundary
- kickstart.nvim demonstrates that a minimal, understandable base is viable

## Consequences

- Must build: module registry, setup/teardown lifecycle, namespace management
- Can still "vendor" selected specs from LazyVim/AstroCommunity
- More upfront work, but maximum long-term durability and debuggability
- No framework-level surprises during reload
