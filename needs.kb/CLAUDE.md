# Needs

What vim must do, organized by function. Each {need}.md describes a functional
need: what it is, how it's currently achieved, what's painful.

Sibling {need}.kb/ directories contain evaluated options for fulfilling that need.

## What Belongs

- {need}.md — one per functional need (editing, navigation, git integration, etc.)
- {need}.kb/{option}.md — one per evaluated option for that need

## What Does NOT Belong

- Guiding principles (→ principles.kb/)
- Adopted choices without alternatives (→ stack.kb/ symlinks)

## Structure

```
needs.kb/
├── {need}.md                 # The need itself
└── {need}.kb/                # Options for fulfilling it
    └── {option}.md           # One evaluated option
```
