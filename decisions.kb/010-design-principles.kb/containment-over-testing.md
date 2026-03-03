# Containment Over Testing

Structural containment (profiles, modularity, bisection) is the primary defense
against config entropy. Tests verify that containment holds — they don't
replace it.

A config that's modular and bisectable is debuggable even without tests. A
config that has 80 tests but is monolithic is still painful to debug when
something unexpected breaks.

Testing a vim config is its own maintenance burden. The goal is high
"invariant-assertion-value per second," not high coverage.

Derives from: config-entropy-compounds, invest-for-durability
