# Reload Safety as Plugin Selection Filter

Every plugin must be either reload-safe or cheaply wrappable to be so. This
follows from idempotent reload being constitutional and teardown being the
framework's primary job.

When evaluating a plugin, ask: "Can I call its setup() twice without
accumulating state? Can I tear down its side effects cleanly?" If the answer
is no and wrapping it is expensive, the plugin is disqualified regardless of
its features.

This is a hard filter, not a preference. A plugin that breaks reload breaks
the development workflow.

Derives from: teardown-is-the-hard-part, editor-state-is-expensive
