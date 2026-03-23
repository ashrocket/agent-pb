# agent-pb

Clipboard butter knife for AI coding agents.

Say `/pb`. The agent finds the most recent useful artifact in your conversation — a query, shell command, code block, URL, or config — and copies it to your clipboard.

No selecting. No highlighting. No dragging.

## Install

### Claude Code (plugin)

```
/plugin marketplace add https://github.com/ashrocket/agent-pb
/plugin install agent-pb@agent-pb-dev
```

### Cursor / Windsurf / Copilot

Copy the portable snippet into your rules file:

```bash
curl -sL https://raw.githubusercontent.com/ashrocket/agent-pb/main/snippets/pb-rules.md >> .cursorrules
```

Or manually paste the contents of [`snippets/pb-rules.md`](snippets/pb-rules.md) into your `.cursorrules`, `.windsurfrules`, or `.github/copilot-instructions.md`.

## Usage

```
/pb                    # copies the most recent useful artifact
/pb the curl command   # copies a specific artifact
```

Works on macOS (`pbcopy`), Linux (`xclip`/`wl-copy`), and WSL (`clip.exe`). Auto-detects your platform.

## Also

- [agent-look](https://github.com/ashrocket/agent-look) — screenshot scanner for Claude. Same philosophy: stop dragging things around.

## License

MIT
