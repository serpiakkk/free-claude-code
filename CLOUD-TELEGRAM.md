# Temporary Free Claude Code Telegram sessions

This fork starts FCC's built-in Telegram bot on demand with GitHub Actions. It is not a permanent service and does not poll on a schedule. To use it, open **Actions → Temporary Telegram coding session → Run workflow**, choose 10–300 minutes, then send a task to the bot's private chat after the run begins. No PC or VPS is needed.

## One-time setup

1. Create a bot with [@BotFather](https://t.me/BotFather), and get your numeric Telegram user ID (for example, with [@userinfobot](https://t.me/userinfobot)).
2. In this repository, open **Settings → Secrets and variables → Actions → New repository secret**, and add:
   - `TELEGRAM_BOT_TOKEN`: your BotFather token.
   - `ALLOWED_TELEGRAM_USER_ID`: your numeric Telegram user ID.
   - `NVIDIA_NIM_API_KEY`: a key from [NVIDIA NIM](https://build.nvidia.com/settings/api-keys), used by the configured model.
   Never put these values in source, issues, workflow inputs, or chat.
3. Keep Actions token permissions read-only. This workflow does not retain a write token, push commits, or automatically publish changes.
4. Start the workflow manually. Cancel it from Actions when you are done.

## Persistence and limits

The checkout, dependencies, Claude session context, and working-tree changes exist only on the temporary runner and disappear when it shuts down. If tracked files change, the workflow tries to save a `session.patch` artifact for one day for your review. It does not apply or publish that patch. A cancellation or failure can lose work that was not exported.

Claude Code can run commands and modify files within the checkout. This is not a sandbox against malicious code or a confidentiality guarantee. Necessary prompts and code are sent through Telegram, FCC, and the AI provider. FCC logs are suppressed from the Actions console, but do not send sensitive data; review every patch before applying it. GitHub and provider limits apply, and availability is not guaranteed.

If GitHub Actions is disabled on this fork, enable it from the **Actions** tab only after reviewing the inherited workflows and this change.
