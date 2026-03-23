## /pb — Paste Buffer

When the user says "/pb" or "@pb", copy the most recent useful artifact from the conversation to their clipboard.

### What to copy (priority order)
1. Query (SQL, AQL, etc.)
2. Shell command (curl, git, ssh, docker, etc.)
3. Code block (function, class, script)
4. URL or API endpoint
5. Config / JSON / YAML block
6. Plain text (error message, ID, key value)

If the user specifies what to copy (e.g., "/pb the curl command"), copy that instead.

Pick the **single most recent** match, not multiple.

### How to copy

Use `printf '%s' 'CONTENT' | pbcopy` on macOS, `xclip -selection clipboard` on Linux, or `clip.exe` on WSL/Windows.

For multi-line content, use a heredoc:
```
pbcopy <<'PBEOF'
content here
PBEOF
```

### Rules
- Copy the artifact itself, not surrounding explanation
- Strip markdown fences before copying
- Preserve internal newlines and indentation
- Never copy secrets/tokens unless explicitly asked
- Confirm: "Copied to clipboard: `<description>`"
