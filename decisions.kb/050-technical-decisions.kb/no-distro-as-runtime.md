# No Distro as Runtime

LazyVim, AstroNvim, LunarVim, and NvChad are not adopted as the runtime
framework. Instead: a bespoke thin orchestrator on top of lazy.nvim.

Distro ecosystems (LazyVim Extras, AstroCommunity) are used as module supply
chains — individual specs can be imported selectively. But the runtime, the
thing that controls load order, lifecycle, and reload, is ours.

lazy.nvim provides plugin loading. kickstart.nvim demonstrates that a minimal,
understandable base is viable. The orchestrator adds module registration,
setup/teardown lifecycle, and namespace management on top.

Follows from: framework-constraints-propagate, teardown-is-the-hard-part
