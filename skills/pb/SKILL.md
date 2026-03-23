---
name: pb
description: This skill should be used when the user says /pb, asks to copy something to the clipboard, paste buffer, or pbcopy, or says "copy that", "grab that command", or "put that in my clipboard". It copies the most recent useful artifact from the conversation to the system clipboard.
user-invocable: true
argument-hint: "[optional: description of what to copy]"
allowed-tools: ["Bash"]
---

# pb — Paste Buffer

Copy the most recent artifact from the conversation that the user is likely to need outside this session.

## What to Copy (Priority Order)

1. **Query** — AQL, SQL, ArangoShell query just written or discussed
2. **Shell command** — curl, git, ssh, aws, artisan, docker command
3. **Code block** — function, class, script, config snippet just written
4. **URL** — endpoint, web URL, API path mentioned
5. **Config / JSON / YAML** — structured data block
6. **Plain text** — error message, key value, ID, filename

If the user provides an argument (e.g., `/pb the curl command`), copy that specific artifact instead of using priority order.

Pick the **single most recent** matching artifact, not multiple.

## How to Execute

First, detect the clipboard command:

```bash
if command -v pbcopy &>/dev/null; then CB="pbcopy"
elif command -v wl-copy &>/dev/null; then CB="wl-copy"
elif command -v xclip &>/dev/null; then CB="xclip -selection clipboard"
elif command -v clip.exe &>/dev/null; then CB="clip.exe"
fi
```

For **single-line content**, use printf (not echo — no trailing newline, no escape interpretation):

```bash
printf '%s' 'CONTENT' | pbcopy
```

**Important:** If content contains single quotes, escape them: replace `'` with `'\''`.

For **multi-line content**, use a heredoc:

```bash
pbcopy <<'PBEOF'
CONTENT_HERE
PBEOF
```

If no clipboard command is available (e.g., remote SSH session), print the artifact in a fenced code block and tell the user to copy manually.

Then confirm in one line:
> Copied to clipboard: `<short description of what was copied>`

## Rules

- Copy the artifact itself — not surrounding explanation or markdown
- Strip markdown fences (` ``` `) before copying
- Preserve internal newlines and indentation in code/config
- If nothing useful exists in the conversation, say so instead of copying noise
- Never copy secrets, tokens, or credentials to clipboard without explicit request
