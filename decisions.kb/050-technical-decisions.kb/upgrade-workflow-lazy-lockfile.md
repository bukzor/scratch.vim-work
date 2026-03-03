# Upgrade Workflow: Lazy.nvim Lockfile

Plugin upgrades are explicit, not automatic. lazy.nvim provides this nearly
for free via `lazy-lock.json`, which pins exact commit SHAs for every plugin.

The lockfile is committed to the repo. Normal usage runs on pinned versions.
`:Lazy update` is run deliberately on "upgrade day," followed by the smoke
and scenario test suites. If something breaks, the lockfile diff shows exactly
what changed.

This eliminates "random Wednesday" breakage where an upstream plugin update
silently introduces an incompatibility.

Follows from: config-entropy-compounds, invest-for-durability
