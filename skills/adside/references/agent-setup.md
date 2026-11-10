<!-- @generated from packages/adside-cli/src/plugin-skills and api-documentation/api-reference/cli-catalog.json by `pnpm docs:generate`. Edit the template, not this file. -->

# Set up an agent to run adside

Share these with the person when `adside` keeps asking for approval or cannot reach Adside. Changing their settings is their call: show the lines, and let them add them.

## Claude Code

Claude Code asks before each `adside` command it has not been allowed to run. To skip the prompt for reads, the person adds exact commands to `permissions.allow` in `~/.claude/settings.json`, or in the project's `.claude/settings.json`:

```json
{
  "permissions": {
    "allow": ["Bash(adside whoami)", "Bash(adside cli search *)"]
  }
}
```

Add a read the team runs often the same way, by its full command, such as `Bash(adside reporting performance query *)`. Never suggest `Bash(adside *)` or a `*` in the middle of a rule: a `*` also matches spaces, so it would allow commands that delete, send or spend.

With Claude Code's sandbox on, `adside` needs `api.adside.ai` and `app.adside.ai` allowed on the network.

## Codex

Codex's default sandbox has no network, so each `adside` call either fails with `fetch failed` or asks for approval. Approving it runs that one command outside the sandbox, where the login works normally.

Do not turn on network access inside the sandbox for `adside`, and do not make `~/.config/adside` writable there instead. Inside the sandbox the login can be read but often not saved, and a refresh that cannot be saved can end the person's CLI logins.

To stop the prompts for reads, the person can add rules to `~/.codex/rules/default.rules`, then restart Codex:

```
prefix_rule(pattern=["adside", "whoami"], decision="allow")
prefix_rule(pattern=["adside", "cli", "search"], decision="allow")
```

Rules match plain commands only: a pipe, a redirect or `$(...)` brings the prompt back.

## Cloud agents and CI

There is no browser to log in with. Install the CLI in the setup script with `npm install -g adside`, store a personal API key (`adside_pat_…`, from **Settings → API keys**, read only when the job allows) as the secret `ADSIDE_API_KEY`, and allow `api.adside.ai` on the network.
