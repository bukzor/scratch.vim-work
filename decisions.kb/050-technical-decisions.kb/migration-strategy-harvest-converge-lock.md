# Migration Strategy: Harvest, Converge, Lock

Unifying the existing branches (multiple prior attempts at rationalizing the
vim config) uses a deliberate extraction process, not branch merging.

**Harvest:** For each branch/attempt, extract only keepers — keymaps, options,
functions that solve real problems. Each item gets: Why (1 line), Tier
(survival/core/full), and Proof (what test would catch regression).

**Converge:** Build the new skeleton first (empty tiered profiles), then
promote harvested items into the correct tier. Migration order: survival kit
first (ruthlessly small), then core, then full. Every migrated item either
has an existing test or justifies a new tiny one.

**Lock:** Tag the result, archive old branches/attempts, commit a short
decisions summary. Stop treating the old configs as living code.

Hard rule: no feature work during migration. Only migrate + delete/park.

Follows from: demand-driven-curation, containment-over-testing,
invest-for-durability
