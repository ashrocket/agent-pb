# agent-pb

Clipboard helper for AI coding agents.

Ask the agent to copy the thing you just produced — a query, shell command, code block, URL, or config — and `agent-pb` puts the artifact itself on your clipboard.

No selecting. No highlighting. No dragging.

## Install

### Claude Code (plugin)

```
/plugin marketplace add ashrocket/agent-pb
/plugin install agent-pb@agent-pb
```

### Codex

Install the bundled skill into your Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills/pb"
curl -sL https://raw.githubusercontent.com/ashrocket/agent-pb/main/skills/pb/SKILL.md \
  -o "${CODEX_HOME:-$HOME/.codex}/skills/pb/SKILL.md"
```

This repo already ships the Codex skill at [`skills/pb/SKILL.md`](skills/pb/SKILL.md).

Useful Codex usage:

```text
$pb
$pb command
$pb the AQL query
copy that
copy the curl command
```

In Codex, `$pb` is the clearest explicit invocation. Natural-language requests also work when the surrounding prompt matches the skill description.

### Cursor / Windsurf / Copilot

Copy the portable snippet into your rules file:

```bash
curl -sL https://raw.githubusercontent.com/ashrocket/agent-pb/main/snippets/pb-rules.md >> .cursorrules
```

Or manually paste the contents of [`snippets/pb-rules.md`](snippets/pb-rules.md) into your `.cursorrules`, `.windsurfrules`, or `.github/copilot-instructions.md`.

## Usage

```
$pb                    # Codex: copies the most recent useful artifact
$pb the curl command   # Codex: copies a specific artifact
/pb                    # slash-style hosts: same behavior
copy that              # natural-language fallback
```

On Codex, the installed skill is designed to trigger on `$pb` and natural-language requests like "copy that", "copy the query", or "grab that command". Treat `/pb` as a compatibility alias for hosts that use slash commands.

Works on macOS (`pbcopy`), Linux (`xclip`/`wl-copy`), and WSL/Windows (`clip.exe`). Auto-detects your platform. Some hosts may require approval before the agent can write to the system clipboard.

## Also

- [agent-look](https://agent-look.raiteri.net) — screenshot scanner for Claude. Same philosophy: stop dragging things around.

## License

MIT
