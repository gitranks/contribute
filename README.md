# GitRanks Contribute

Your coding agent works on open-source issues picked for you. You review every change and approve the pull request on
[gitranks.com](https://gitranks.com/contribute), and it opens under your name.

This repository connects your own agent (Claude Code, Codex, Cursor, Gemini CLI and others) to the GitRanks Contribute
MCP server at `https://mcp.gitranks.com/mcp`, and adds a `contribute` skill that walks it through one issue. It holds
only configuration and instructions: the server runs on GitRanks.

GitRanks Contribute is in beta. It is free.

## Before you start

1. Sign in on [gitranks.com/contribute](https://gitranks.com/contribute) with GitHub.
2. In **Contribute → Settings → Your own agent (MCP)**, create a token. It starts with `gr_`.

## Install

### Claude Code

```bash
claude plugin marketplace add gitranks/contribute
claude plugin install gitranks-contribute@gitranks
```

Claude Code asks for your token when the plugin is enabled and keeps it in your system keychain.

### Gemini CLI

```bash
gemini extensions install https://github.com/gitranks/contribute
```

Gemini CLI asks for your token (`GITRANKS_MCP_TOKEN`) and keeps it in your system keychain.

### Antigravity

Add the `gitranks` entry to Antigravity's MCP config, `~/.gemini/config/mcp_config.json`. In the IDE, open it from the
… menu at the top of the agent panel → MCP Servers → Manage MCP Servers → View raw config.

```json
{ "mcpServers": { "gitranks": { "serverUrl": "https://mcp.gitranks.com/mcp", "headers": { "Authorization": "Bearer <your GitRanks token>" } } } }
```

Antigravity can't read environment variables in this file yet, so the token sits in it: keep the file to yourself.
Then refresh its MCP servers: in the app, the refresh button under Settings → Customizations → Installed MCP Servers;
in the CLI, `/mcp`.

### Codex, Cursor and others

Save the token in your environment as `GITRANKS_MCP_TOKEN`, then add the server:

- **Codex** (`~/.codex/config.toml`):

  ```toml
  [mcp_servers.gitranks]
  url = "https://mcp.gitranks.com/mcp"
  bearer_token_env_var = "GITRANKS_MCP_TOKEN"
  ```

- **Cursor** (`~/.cursor/mcp.json`):

  ```json
  { "mcpServers": { "gitranks": { "url": "https://mcp.gitranks.com/mcp", "headers": { "Authorization": "Bearer ${env:GITRANKS_MCP_TOKEN}" } } } }
  ```

- **Any MCP client** with streamable HTTP: URL `https://mcp.gitranks.com/mcp`, header `Authorization: Bearer <your token>`.

The skill in `skills/contribute/SKILL.md` works in any agent that reads Agent Skills.

## Use it

Ask your agent: "Find me an open-source issue to work on with GitRanks." It lists issues picked for you, claims the one
you choose, fixes it on your machine and hands the change back. Then review it and approve the pull request on
gitranks.com.

In Claude Code the plugin adds two commands:
- `/gitranks-contribute:find [language, kind or owner/repo]`: issues picked for you, then work on the one you choose;
- `/gitranks-contribute:status`: your claims and pull requests, and what each one needs from you.

## What is sent to GitRanks

Everything goes to `mcp.gitranks.com`, authenticated with your token:
- the filters you ask `find_issues` for;
- the issue you claim or give back, with your note;
- the change you hand back: the patch (`git format-patch`), your agent's summary and brief, and the tests it ran with
  their output;
- for a follow-up, your agent's replies to the review;
- what your agent learned about how a repository builds and tests;
- screenshots, when your agent captures a proof of a change's behaviour.

Your agent, its model and your code editor stay on your machine. GitRanks never sees your other files or your
model's API key. See the [privacy policy](https://gitranks.com/privacy) and the
[maintainers' page](https://gitranks.com/contribute/maintainers) for what GitRanks does with a change and how a
repository can opt out.

## License

MIT
