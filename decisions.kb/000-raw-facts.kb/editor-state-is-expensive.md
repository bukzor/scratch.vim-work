# Editor State Is Expensive to Rebuild

Restarting the editor mid-flow loses buffer state, window layout, undo history,
and mental context. The cost is real and recurring — it's paid every time a
config change requires a restart to take effect.

This makes in-process reload a high-value capability, not a luxury.
