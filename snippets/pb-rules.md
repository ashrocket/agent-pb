## /pb — Paste Buffer

When the user says "$pb", "/pb", "copy that", "gimme that", or asks to copy something from the conversation, copy it to their clipboard.

### Select

With args: match by type ("command"), description ("the AQL query"), or ordinal ("2" = 2nd most recent). Without args, pick most recent: query > shell command > code block > URL > config > plain text.

Ordered sequences: copy first-to-run, not last.

### Copy

Detect platform: `pbcopy` (macOS), `wl-copy` / `xclip -selection clipboard` (Linux), `clip.exe` (WSL). Assign to `$CB`. Single-line: `printf '%s' 'CONTENT' | $CB`. Escape `'` as `'\''`. Multi-line: heredoc with `$CB <<'PBEOF'`.

### Rules

- Strip markdown fences and trailing newlines, copy raw content only
- Preserve internal newlines/indentation
- Never copy secrets without explicit request
- If no clipboard command found, print artifact in a fenced code block for manual copy
- If no useful artifact exists, say so — don't copy noise
- One-line confirmation: `Copied to clipboard: <description>`
