# KB and ADR Formats Serve Different Purposes

**Date:** 2026-03-02
**Status:** Accepted

## Context

We have two documentation patterns in play: the `.kb/` pattern (small focused
files, categorical nesting, descriptive names) and the ADR pattern (temporal
ordering, structured sections: status/context/alternatives/decision/consequences).

An early attempt placed ADR-formatted documents inside `decision-records.kb/`
(a symlink to `docs/dev/adr/`). This created tension — the ADR format's rigid
sections and date-prefixed naming fought the kb pattern's categorical nesting
and prose-focused style.

## Decision

Keep ADR format and kb format as separate systems with distinct purposes:

- **`docs/dev/adr/`** — Process and methodology decisions, using ADR format
  (temporal, flat, structured sections). For decisions about *how we work*.
- **`decisions.kb/`** — Product/technical knowledge, using kb format (categorical,
  nested, prose). For decisions about *what we're building*.

The `decision-records.kb` symlink is removed. ADR format does not enter `.kb/`
directories.

## Alternatives Considered

### Unify everything into ADR format inside .kb/
- **Pros:** One system, one format
- **Cons:** ADR ceremony (status/alternatives/consequences sections) is overhead
  for value statements and design principles. Date-prefix naming fights
  categorical organization. The formats optimize for different reading patterns.

### Unify everything into kb format, drop ADRs
- **Pros:** Simpler, consistent
- **Cons:** Loses the structured alternatives analysis that ADRs provide for
  contested process decisions. ADR format is genuinely useful when the primary
  value is "what else did we consider and why not."

## Consequences

**Positive:**
- Each format used where it fits naturally
- `decisions.kb/` can nest by abstraction level (000/010/050) without fighting
  temporal ordering
- ADRs remain available for process decisions where structured alternatives
  analysis matters

**Negative:**
- Two systems to understand instead of one
- Must decide which system a given decision belongs to

## Related

- Supersedes: the `decision-records.kb -> docs/dev/adr` symlink approach
