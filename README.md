# Agent TG Skills

Open-source skills for AI coding agents, from the Agent TG channel.

Each skill is a folder of plain Markdown. It teaches an agent a process that worked for me on a real project. They run in Claude Code and Codex.

## Skills

| Skill | What it does |
| --- | --- |
| [implicit-state-machines](skills/implicit-state-machines/) | Finds the bugs hiding in your app's multi-step flows (save, upload, sync, delete, refresh), plans the fixes with you, then fixes them through tested and reviewed steps. |

## Install a skill

Copy the skill's folder from `skills/` into your agent's skills directory.

- **Claude Code:** `~/.claude/skills/`
- **Codex:** `~/.codex/skills/`

Start a new session in your project. Each skill's own README shows the prompt that starts it.

## What to expect

- Every skill here came from real work. I removed the private details before sharing it.
- Skills follow your project's own rules for testing, review and release. They give the agent no authority of its own.
- They are starting points. Expect to adapt them to your project.

## License

MIT. See [LICENSE](LICENSE).
