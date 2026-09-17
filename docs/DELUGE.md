# DELUGE

Three Zoho Cliq Deluge scripts. Deluge is Zoho's scripting language for building logic inside Zoho products (Cliq bots, Creator apps, etc.); these three files are Cliq bot command handlers.

## Files

### `SHOT BOT x DELUGE.txt` — Shot Engine v1.x bot handler

The main bot logic: parses an incoming Cliq message, extracts a model keyword and prompt (falling back to a default model, `#gemini`, when the user gives a single word with no explicit model prefix), and routes the request accordingly. Marked as a prototype version built for a "CliqTrix '26" submission, with API keys explicitly stripped from the committed file.

### `SHOT SLASH x DELUGE.txt` — `/shot` slash command

A lighter companion handler: responds to the `/shot` slash command with an overview of and link to the Shot v1.x bot, rather than processing a full conversational prompt. Calls the Gemini API directly (`gemini-2.0-flash`) via `generativelanguage.googleapis.com`, with the API key placeholdered as the literal string `"GEMINI_API_KEY"` rather than a real value in the committed version.

### `SNIPER x DELUGE.txt` — Auth0 login handler

This is very likely the actual Deluge auth layer referenced in the ZOHO-AUTH0 project's "SNIPER Engine" install flow documented earlier: an on-demand-login Auth0 token vault. Configuration values (`AUTH0_DOMAIN`, `AUTH0_CLIENT_ID`, `AUTH0_AUDIENCE`, `REDIRECT_URI`) are placeholdered (`<auth0>`, `<auth0_Client_ID>`, etc.) in the committed file, not real values.

## Security note: these files are safe to commit as-is

All three files have their real credentials already stripped and replaced with placeholders or literal string markers before being committed here. That's the right pattern to keep going: if you ever paste a working copy with real keys into this folder temporarily for local testing, strip them back out (or better, keep the real-keys copy entirely outside this repo) before committing, the same way these three already are.

## Deploying these

These are Deluge scripts, not standalone-runnable Python/JS files: they only execute inside the Zoho Cliq platform, wired to a bot's command/message handlers through the Cliq bot builder or the Zoho Extension Toolkit. See the ZOHO-AUTH0 project's `.zoho/` documentation (built earlier in this delivery series) for the general shape of that packaging, if you're formalizing these into a proper Cliq extension rather than pasting them directly into the Cliq bot builder UI.
