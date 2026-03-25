---
name: pb
description: Use when the user types $pb, /pb, or asks to copy something from the conversation to the clipboard, such as "copy that", "copy the query", "grab that command", or "gimme that". Copies the selected artifact to the system clipboard.
---

Copy the artifact to clipboard. Be fast — no explanation, no preamble.

## Select

With args: match by type ("command"), description ("the AQL query"), or ordinal ("2" = 2nd most recent).

Without args, pick most recent: query > shell command > code block > URL > config > plain text.

Ordered sequences: copy first-to-run, not last.

## Copy

```bash
if command -v pbcopy &>/dev/null; then CB="pbcopy"
elif command -v wl-copy &>/dev/null; then CB="wl-copy"
elif command -v xclip &>/dev/null; then CB="xclip -selection clipboard"
elif command -v clip.exe &>/dev/null; then CB="clip.exe"; fi
```

Single-line: `printf '%s' 'CONTENT' | $CB` (escape `'` as `'\''`)

Multi-line: heredoc with `$CB <<'PBEOF'`

## Rules

- Strip markdown fences, copy raw content only
- Preserve newlines/indentation
- Never copy secrets without explicit request
- If no clipboard command found, print artifact in a fenced code block and tell user to copy manually
- If no useful artifact exists, say so — don't copy noise
- One-line confirmation only: `Copied to clipboard: <description>`
