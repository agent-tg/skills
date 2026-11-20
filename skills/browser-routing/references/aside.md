# Aside background browser

[Aside](https://aside.com) is a browser built for agents. It has its own window, its own signed-in sessions and a built-in password manager. Your agent controls it in the background through Aside's MCP server or its `aside repl` command, so your own browser and screen stay yours.

## Use it

Prefer the MCP tool. In Claude Code it is usually `mcp__aside__repl`; in Codex it shows up in the tool list as the Aside `repl` tool. If MCP is not connected, run one bounded command instead:

```bash
aside repl "const p = await openTab('https://example.com'); console.log(await p.title());"
```

Rules:

- Work with page actions (open tab, read the page, click by reference, fill a field). Read pages with `snapshot(page)` or the page text before taking screenshots.
- Open your own tabs and close them when done. Leave the user's own Aside tabs alone unless they asked you to use one.
- Keep each command short and finished. Do not leave a long-running browser session open.
- In my use, plain page control has not used Aside credits. Running Aside's own AI agent (`aside "<task>"` or `aside exec`) does use credits. Only do that if the user asks for it.
- For a local dev server, open `http://localhost:<port>` in Aside instead of letting the dev server pop open the user's browser.

## Quick setup check

```bash
aside repl 'const t = await listBrowserTabs(); console.log(JSON.stringify({connected: true, tabs: t.length}));'
```

If this prints `connected: true`, the agent can reach Aside. It does not prove any site is signed in.

## Install (once)

1. Download Aside from [aside.com](https://aside.com) and sign in. The Free plan works for this skill.
2. Install the CLI:

   ```bash
   curl -fsSL https://releases.aside.com/install.sh | bash
   ```

   (Aside's Developer settings can also install it. On Windows, use the PowerShell steps under the Windows tab in [Aside's docs](https://docs.aside.com/help/developers).)
3. Connect it to your agent as an MCP server:

   ```bash
   claude mcp add --scope user aside -- aside mcp
   ```

   ```bash
   codex mcp add aside -- aside mcp
   ```

   For other tools that read `mcp.json`:

   ```json
   { "mcpServers": { "aside": { "command": "aside", "args": ["mcp"] } } }
   ```
4. Sign in to the sites you want the agent to use, once, inside Aside.

Aside's docs: [Use the CLI, MCP, and REPL](https://docs.aside.com/help/developers).
