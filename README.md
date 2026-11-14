# Adside plugin for Claude Code and Codex

Teaches an AI agent to run your Adside workspace from your computer, with the `adside` command line and the Adside MCP server.

- **`adside`**: when to use the command line or the MCP, how to install and log in, how to find a command with `adside cli search`, and what needs your OK before it runs.
- **`adside-media`**: image, video and audio generation, priced before anything is paid.
- **`adside-assets`**: uploading, downloading and organizing the asset library.
- **The Adside MCP server** (`https://api.adside.ai/mcp`), which signs in with your browser the first time it is used.

This repository also holds **Adside Creative** (`adside-creative/`), a plugin for making ad creatives from Claude on claude.ai, in Cowork and in Claude Code, through the Adside MCP alone. See [its README](adside-creative/README.md). In Claude Code:

```bash
claude plugin install adside-creative --marketplace AgenticAdvertising/adside-plugin
```

## Install

Claude Code:

```bash
claude plugin install adside --marketplace AgenticAdvertising/adside-plugin
```

Codex:

```bash
codex plugin marketplace add AgenticAdvertising/adside-plugin
```

```bash
codex plugin add adside@adside
```

The plugin does not include the command line. Install it with `npm install -g adside` (Node.js 22 or later); it updates itself.

Setup and the full guide: [docs.adside.ai/cli/agent-plugin](https://docs.adside.ai/cli/agent-plugin).

## What it is allowed to do

The command line and the API make a change on the first call, with no confirmation step, so the skills tell the agent to ask you before anything that creates, changes, deletes, sends or spends. On ad platforms the command line only reads; changes go through the MCP, which asks for a confirmation first. The agent acts as you, with your permissions. For a headless agent, use a read-only personal API key.

## Working on it

`AgenticAdvertising/adside-plugin` is a copy of `plugins/adside` (the repository root) and `plugins/adside-creative` (`adside-creative/`) in Adside's main repository: a change made only here is lost at the next copy.

The skills under `skills/` are generated: edit the templates in `packages/adside-cli/src/plugin-skills/`, then run `pnpm docs:generate`. Command lists come from the CLI's catalog, and the generator refuses a template that names a command the published CLI does not have.

Check the plugin with:

```bash
claude plugin validate plugins/adside --strict
```
