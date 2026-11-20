# Browser Routing

A skill for AI coding agents. It gets your agent into websites the easy way, and when it does need a browser, it uses one that runs in the background so you can keep using your computer.

It's my most used skill.

This is a slim version of the one I run. Mine also has 10 helper skills for things like email, downloads and login codes. Those are tied to my own setup, so they aren't included here.

## The problem

You ask your agent to grab something from a website. It opens your browser and takes over your screen. You were kind of using that.

## What it does

1. **Easy way first.** Before it touches a browser, the agent checks for an API, a CLI, a connector, an MCP tool, an export, or a plain page fetch. Most jobs end here.
2. **Background browser second.** If it really needs a browser (a login, a dashboard, a form, a download), it drives [Aside](https://aside.com) in the background. Your own browser and screen stay yours.
3. **Stays signed in.** Aside keeps its own sessions, so the agent isn't asking you to log in every time. Passwords fill from a password manager and never show up in the chat.

I use it for pretty much any website: reading an X post or a YouTube video, pulling reports out of a dashboard, downloading invoices, setting things up in Slack.

## What to install

| What | Needed? | Cost |
| --- | --- | --- |
| This skill | Yes | Free (MIT) |
| [Aside](https://aside.com) browser, signed in | Yes | The Free plan works. In my use, driving pages with this skill hasn't used Aside credits. Aside's own AI agent does use credits (500 a month on Free). Paid plans start at $20/month if you want more. |
| Aside CLI + MCP server | Yes | Free, comes with Aside. Setup in [references/aside.md](references/aside.md). |
| [1Password](https://1password.com) CLI + a service account | Optional, advanced | Needs a paid 1Password account. Setup in [references/1password.md](references/1password.md). |

Prices checked on aside.com on November 19, 2026.

## Install

1. Install Aside and sign in. Then install the CLI and connect it to your agent:

   ```bash
   curl -fsSL https://releases.aside.com/install.sh | bash
   ```

   ```bash
   claude mcp add --scope user aside -- aside mcp
   ```

   For Codex: `codex mcp add aside -- aside mcp`

   On Windows, the CLI install is a PowerShell script instead of the `curl` line. Use the Windows tab in [Aside's install steps](https://docs.aside.com/help/developers). I haven't tested this skill on Windows.

2. Copy this `browser-routing` folder into your agent's skills folder:
   - **Claude Code:** `~/.claude/skills/`
   - **Codex:** `~/.codex/skills/`

3. Add this 1 line to your `CLAUDE.md` or `AGENTS.md`:

   ```text
   For any website or browser task, use the browser-routing skill: try an API or connector first, then the Aside background browser. Never take over my own browser.
   ```

4. Start a new session. Sign in to the sites you want your agent to use, once, inside Aside.

## Advanced: 1Password

My agent has its own 1Password account, so it only sees the logins I share with it. You don't need that on day one. Start with Aside's built-in password manager. When you want it, follow [references/1password.md](references/1password.md).

## What's inside

- `SKILL.md`: the route order, logins, safety rules.
- `references/aside.md`: how the agent drives Aside, a setup check, and install steps.
- `references/1password.md`: the optional 1Password add-on.

## Limits

- The route can be right and the answer can still be wrong. Ask for the link behind what it brings back, and check it.
- Aside is a separate browser. Sign in to your sites there once; it doesn't share your main browser's logins unless you import them.
- It asks before sending, posting, buying or deleting anything. It won't solve CAPTCHAs or reset passwords.
- It's instructions, not permissions. Installing it gives the agent no new accounts or access.
- I've run it on my own setup (Mac, Claude Code and Codex). Expect to adapt it to yours.

## License

MIT. See [LICENSE](../../LICENSE).
