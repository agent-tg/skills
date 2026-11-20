# Optional: 1Password for your agent

Skip this on day one. Aside's built-in password manager is enough to start.

This add-on gives your agent its own 1Password **service account**. It can only see the vaults you share with it, so it never sees your personal logins.

## Set it up

1. In 1Password, make a vault just for agent logins (for example `Agent Logins`). Move or copy in only the logins the agent should use.
2. Create a service account with read access to that vault only. ([1Password service accounts](https://developer.1password.com/docs/service-accounts/get-started/))
3. Install the 1Password CLI (`op`). ([Install the CLI](https://developer.1password.com/docs/cli/get-started/))
4. Put the service account token in the environment your agent runs in as `OP_SERVICE_ACCOUNT_TOKEN`. Keep it out of project files, Git and chat.

## How the agent uses it

- Find the item by name: `op item list --vault "Agent Logins"`. Item names and usernames are fine to show. Passwords are not.
- Read a value straight into the place that needs it, never into the chat. For a login form in Aside, read the password inside the same command that fills the field, and do not print it.
- For apps that read secrets from the environment, use `op run` with `op://vault/item/field` references so the real value never appears in a command or file.
- For an authenticator code stored in 1Password: `op item get "<item>" --vault "Agent Logins" --otp`, used once for the login in progress.

## Rules

- Never print, log, screenshot, commit or save a secret value.
- If the item is missing or the vault is not shared, stop and tell the user which login is needed. Do not ask them to paste the password into chat.
- Never create, edit or delete vault items unless the user asks.

Check 1Password's site for which plans include service accounts.
