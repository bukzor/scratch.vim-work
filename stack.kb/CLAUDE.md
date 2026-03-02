# Stack

Symlink farm to chosen options in needs.kb/{need}.kb/. Each symlink names
the need and points to the winning option.

`ls -la` answers "what did I choose and where's the rationale."

Broken symlinks signal stale decisions.

## What Belongs

Symlinks only. One per need, pointing to the chosen option:

```
stack.kb/
├── syntax-highlighting.md -> ../needs.kb/syntax-highlighting.kb/treesitter.md
├── plugin-management.md   -> ../needs.kb/plugin-management.kb/lazy-nvim.md
```

## What Does NOT Belong

- Regular files (all content lives in needs.kb/)
- Multiple symlinks per need (that's an unresolved decision, not a stack choice)

## Alternative Stacks

Additional symlink farms (e.g. stack-minimal.kb/, stack-ssh.kb/) can represent
alternative configurations for comparison or different environments.
