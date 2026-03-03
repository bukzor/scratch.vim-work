# Portability, Not Vim-Compatibility

Portability is the real value. Vim-compatibility is only one way to achieve it.

Because environments are diverse and unpredictable, the config must work across
them. But "works across environments" doesn't require "everything runs in plain
vim." It requires a dependency-free baseline that works anywhere, and a richer
config that works where neovim is available.

Conflating portability with vim-compat led to a blanket constraint that taxed
every config decision for 18 years while being rarely exercised.

Derives from: diverse-environments, config-entropy-compounds
