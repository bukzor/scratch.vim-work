# Teardown Is the Hard Part of Reload

Most setup operations are naturally idempotent — setting an option twice does
the same thing. The real obstacle to reload is accumulated side effects:
duplicate autocommands, orphaned user commands, stale keymaps, leaked timers.

If teardown is easy and reliable, reload follows. If teardown is hard, no
amount of clever setup logic helps.

This means the framework's primary job is making side effects discoverable
and removable — through ownership namespaces, explicit registration, and
standard cleanup helpers.

Derives from: editor-state-is-expensive
