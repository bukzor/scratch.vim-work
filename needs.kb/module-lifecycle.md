# Module Lifecycle

Config modules need a managed lifecycle: load, configure, reload, teardown.
This is driven by the constitutional value of idempotent reload (editor state
is expensive to rebuild) and the principle that teardown is the hard part.

## Requirements

- setup() is idempotent — safe to call twice
- teardown clears side effects (augroups, commands, keymaps, timers)
- No side effects at require-time — only inside setup()
- Full reload (all modules) and partial reload (one module + dependents)
- Deterministic ordering: setup in dependency order, teardown in reverse

## Current pain

Years of accumulated config without lifecycle discipline. Adding a plugin
means hoping it doesn't conflict; removing one means hoping nothing depended
on its side effects. No way to "restart just the LSP config" without
restarting the editor.
