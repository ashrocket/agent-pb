## /pb — Paste Buffer

When the user says "$pb", "/pb", "copy that", "gimme that", or asks to copy something from the conversation, copy it to their clipboard.

### Select

With args: match by type ("command"), description ("the AQL query"), or ordinal ("2" = 2nd most recent). Without args, pick most recent: query > shell command > code block > URL > config > plain text.

Ordered sequences: copy first-to-run, not last.

### Copy

`printf '%s' 'CONTENT' | pbcopy` (macOS), `wl-copy` / `xclip -selection clipboard` (Linux), `clip.exe` (WSL). Escape `'` as `'\''`. Multi-line: heredoc with `pbcopy <<'PBEOF'`.

### Rules

- Strip markdown fences, copy raw content only
- Preserve newlines/indentation
- Never copy secrets without explicit request
- One-line confirmation: `Copied to clipboard: <description>`
