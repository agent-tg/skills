---
name: browser-routing
description: "Browser Routing: reach websites the easy way first (API, CLI, connector, MCP tool, export or plain page fetch), and only then use the Aside browser running in the background, so the agent never takes over the user's screen. Use for any website, web app, dashboard, login, download, screenshot, localhost check, or shared X/YouTube/web link."
---

# Browser Routing

Get into a website the easy way first. Use a browser only when nothing easier finishes the job, and then use one that runs in the background so the user keeps their screen.

## 1. Pick the route

Go down this list and stop at the first route that finishes the task.

1. **Something you already have.** A connector, MCP tool, CLI, API, or export that covers this site (for example a GitHub CLI, a Slack or Google connector, a site's official API). Check the tools you have before opening any page.
2. **A plain fetch.** For public pages: fetch the page or its text. For YouTube, get the transcript or captions. For an X post, try the page text or a reader service before a browser.
3. **The Aside background browser.** When the site needs a signed-in session, clicks, forms, a dashboard, a download behind a login, or a screenshot. See [references/aside.md](references/aside.md).
4. **Anything else** (taking over the user's own browser, screen control, another browser extension). Only with the user's clear OK in the current conversation. Say why the routes above did not work.

Never open or drive the user's personal browser window, steal focus, or move their mouse and keyboard to finish a web task.

## 2. Keep the task in view

Before you start, know: the goal, which site and account, and what "done" looks like (a file saved, a setting changed, a number read). Ask one short question only when a wrong guess would change the result, such as which of two accounts to use. Otherwise decide and say what you picked.

Logging in is a step, not the finish. After you get back in, go back and finish the original task.

## 3. Logins

- Aside keeps its own signed-in sessions. Reuse them. An expired session is normal: sign back in and continue.
- When a password is needed, let Aside's built-in password manager fill it, or use the optional 1Password setup in [references/1password.md](references/1password.md). The agent should fill the field without the password appearing in the chat.
- One-time codes: use an authenticator code from the password manager when one is stored there. Otherwise ask the user for the code. Only use a code for the login you are doing right now.
- Never guess passwords, reset a password, turn off two-step login, or change account roles to get past a failure. Ask the user.

## 4. Safety

- Passwords, codes, tokens and cookies never go in chat output, logs, screenshots, command arguments or saved files.
- Reading is fine. Sending, posting, buying, deleting, or changing account settings needs the user's OK for that exact action, unless they already asked for it.
- Use only the accounts the user pointed you to. Do not sign up for anything or accept terms on their behalf without asking.
- Check the result where it counts: the page after the change, the downloaded file, the real report. "I clicked save" is not proof.
- After two real failures on the same problem, stop and tell the user what you saw and what the choices are.
- Close the tabs you opened. Delete any temporary file that held a secret.

## 5. Check the source

Getting into the site the right way does not make the answer right. When you bring back facts from a page or video, include the link (and timestamp for video) so the user can check it.

This skill is instructions only. Installing it gives the agent no new accounts, passwords or permissions.
