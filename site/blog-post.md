# I built a butter knife for your AI agent's clipboard

There are probably a million reasons why I shouldn't have built this. If you know any, leave a comment below.

---

Here's my workflow, dozens of times a day: I ask Claude to write a query, or a curl command, or a function. Claude writes it. Then I have to select the text — carefully, because the markdown fences aren't part of it — copy it, switch to my terminal or editor, and paste.

It's not hard. It's just *constant*. And every time I do it I think: you're an AI agent with access to my shell. Why am I the one doing this?

So I built **agent-pb** — a clipboard butter knife. You say `/pb` and the agent finds the most recent useful thing in your conversation — a query, a shell command, a code block, a URL — and spreads it right into your clipboard. No selecting. No highlighting. You just paste.

---

The metaphor came naturally. pb is the macOS clipboard command (`pbcopy`/`pbpaste`), but it's also how the tool feels. You're not carefully cutting and placing text — you're just spreading it where it needs to go, like butter on toast.

---

The interesting design decision was making it portable. agent-pb is a proper Claude Code plugin, but the core of it is just a prompt and a shell command. There's nothing Claude-specific about "find the most recent useful artifact and pipe it to the clipboard."

So the GitHub repo includes a portable snippet — drop it into your `.cursorrules`, `.windsurfrules`, `.github/copilot-instructions.md`, or whatever your agent reads. Same butter knife, different bread.

Cross-platform too: `pbcopy` on macOS, `xclip` on Linux, `clip.exe` on WSL. The skill auto-detects.

---

This is the second tool in what I'm calling the **agent-\*** family. The first was [agent-look](https://agent-look.pages.dev) — a screenshot scanner that lets you say `/look` instead of dragging image files into Claude.

Same philosophy: stop moving things around manually. Let the agent handle the boring mechanical parts so you can stay in flow.

---

**Get it:** [github.com/ashrocket/agent-pb](https://github.com/ashrocket/agent-pb)

If something's broken, file an issue. If it works perfectly, I will accept quiet gratitude.
