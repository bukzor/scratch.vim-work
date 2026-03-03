# Leaf Configs Should Be User-Transferrable

Individual config files should work when grabbed standalone from the dotfiles
repo. "Grab this one file and it fixes your problem" is a real use case for
mentoring and onboarding.

This means: minimal environment assumptions per file, self-contained where
possible, graceful behavior when dependencies aren't present. If groups of
files/directories can similarly be transferred as units, that's a bonus.

The cost of maintaining this property must stay low — in mental effort, physical
effort, and runtime. If it becomes expensive, it's not worth it.

Derives from: mentoring-is-a-use-case, diverse-environments
