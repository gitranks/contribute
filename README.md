# GitRanks Contribute

Your coding agent works on open-source issues picked for you. You review every change and approve the pull request on
[gitranks.com](https://gitranks.com/contribute), and it opens under your name.
Every pull request opened from gitranks.com says it was made with GitRanks Contribute and your agent (with its model
when the agent reports one), and links where maintainers can tell us something is off or opt out.

This repository connects your own agent (Claude Code, Codex, Cursor, Gemini CLI and others) to the GitRanks Contribute
MCP server at `https://mcp.gitranks.com/mcp`, and adds a `contribute` skill that walks it through one issue. It holds
only configuration and instructions: the server runs on GitRanks.

GitRanks Contribute is in beta. It is free.

## How you connect

Add the server's URL to your agent, then sign in. The first time your agent connects, it opens gitranks.com in your
browser: sign in with GitHub, check what the agent will be able to do, and press **Allow**. Your agent keeps the access
it gets and renews it by itself while you use it. Nobody copies a token.

Each agent you connect is listed on gitranks.com under **Contribute → Settings → Your own agent (MCP)**, where you can
disconnect it at any time.

A client that can't sign in can still use a personal token: see [Use a token instead](#use-a-token-instead).

## Install

### Claude Code

```bash
claude plugin marketplace add gitranks/contribute
claude plugin install gitranks-contribute@gitranks
```

If Claude Code offers a token field when the plugin is enabled, leave it empty: it is optional. Then run `/mcp`, pick
the `gitranks` server, choose **Authenticate** and sign in on gitranks.com.

Without the plugin: `claude mcp add --transport http gitranks https://mcp.gitranks.com/mcp`, then `/mcp` → `gitranks` →
**Authenticate**.

### Gemini CLI

```bash
gemini extensions install https://github.com/gitranks/contribute
```

Gemini CLI asks for an optional token: leave it empty. Then run `/mcp auth gitranks` and sign in on gitranks.com.

Without the extension: `gemini mcp add --transport http gitranks https://mcp.gitranks.com/mcp`, then
`/mcp auth gitranks`.

### Codex

```bash
codex mcp add gitranks --url https://mcp.gitranks.com/mcp
codex mcp login gitranks
```

### Cursor, VS Code and others

Add the server by its URL alone; the editor offers to sign in when it first connects.

- **Cursor** (`~/.cursor/mcp.json`):

  ```json
  { "mcpServers": { "gitranks": { "url": "https://mcp.gitranks.com/mcp" } } }
  ```

- **Any MCP client** with streamable HTTP and sign-in: URL `https://mcp.gitranks.com/mcp`, nothing else.

This repository is also an [Agent Plugins](https://github.com/agentplugins/agent-plugins-spec) package (`plugin.json`
and `mcp.json` at its root, plus the skill), for clients and marketplaces that install that format. It carries the URL
only, so it connects by signing in.

### Claude Desktop and claude.ai

Settings → Connectors → Add custom connector, with the URL `https://mcp.gitranks.com/mcp`. Then connect it and sign in.

### Antigravity

Antigravity connects with a token for now: see [Use a token instead](#use-a-token-instead).

The skill in `skills/contribute/SKILL.md` works in any agent that reads Agent Skills.

## Use a token instead

For a client without sign-in, or a script, create a personal token on
[gitranks.com/contribute](https://gitranks.com/contribute) under **Contribute → Settings → Your own agent (MCP)**. It
starts with `gr_`. Send it in the `X-GitRanks-Token` header, or as `Authorization: Bearer <your token>`. Keep it to
yourself: it acts as you until you revoke it there.

- **Claude Code plugin:** set the plugin's token option (in `/plugin`, open GitRanks Contribute and configure it).
  Claude Code keeps it in your system keychain and sends it in `X-GitRanks-Token`.
- **Gemini CLI extension:** give the token when it asks, or later with
  `gemini extensions config gitranks-contribute "GitRanks token"`. Gemini CLI keeps it in your system keychain
  (`GITRANKS_MCP_TOKEN`) and sends it in `X-GitRanks-Token`.
- **Codex** (`~/.codex/config.toml`), with the token in your environment as `GITRANKS_MCP_TOKEN`:

  ```toml
  [mcp_servers.gitranks]
  url = "https://mcp.gitranks.com/mcp"
  bearer_token_env_var = "GITRANKS_MCP_TOKEN"
  ```

- **Cursor** (`~/.cursor/mcp.json`), with the token in your environment as `GITRANKS_MCP_TOKEN`:

  ```json
  { "mcpServers": { "gitranks": { "url": "https://mcp.gitranks.com/mcp", "headers": { "Authorization": "Bearer ${env:GITRANKS_MCP_TOKEN}" } } } }
  ```

- **Any MCP client** with streamable HTTP: URL `https://mcp.gitranks.com/mcp`, header `Authorization: Bearer <your token>`.

- **Antigravity:** add the `gitranks` entry to its MCP config, `~/.gemini/config/mcp_config.json`. In the IDE, open
  it from the … menu at the top of the agent panel → MCP Servers → Manage MCP Servers → View raw config.

  ```json
  { "mcpServers": { "gitranks": { "serverUrl": "https://mcp.gitranks.com/mcp", "headers": { "Authorization": "Bearer <your GitRanks token>" } } } }
  ```

  Antigravity can't read environment variables in this file yet, so the token sits in it: keep the file to yourself.
  Then refresh its MCP servers: in the app, the refresh button under Settings → Customizations → Installed MCP
  Servers; in the CLI, `/mcp`.

## Use it

Ask your agent: "Find me an open-source issue to work on with GitRanks." It lists issues picked for you, claims the one
you choose, fixes it on your machine and hands the change back. Then review it and approve the pull request on
gitranks.com.

In Claude Code the plugin adds two commands:
- `/gitranks-contribute:find [language, kind or owner/repo]`: issues picked for you, then work on the one you choose;
- `/gitranks-contribute:status`: your claims and pull requests, and what each one needs from you.

## What is sent to GitRanks

Everything goes to `mcp.gitranks.com`, except the sign-in page and your approvals, which are on `gitranks.com`.

When you sign in:
- your agent registers itself: the name it gives itself and the address the sign-in answer goes back to (on your
  computer, or the client's own page). The consent page shows both;
- you sign in to gitranks.com with GitHub, and press Allow. Your agent then gets an access token and a refresh token
  from `mcp.gitranks.com`, which it sends with every call and uses to renew its access.

With every tool call, the access token (or your personal token, when you use one), and:
- the filters you ask `find_issues` for;
- the issue you claim or give back, with the reason and your note;
- the change you hand back: the patch (`git format-patch`), your agent's verdict, summary and brief, the tests it ran
  with their output, its risk notes, and the pull request title and text it suggests;
- your agent's name and the model it runs on, as it reports them with a change or a proof;
- for a follow-up, what you asked for in your own words, and your agent's reply drafts to the review;
- what your agent learned about how a repository builds and tests;
- for a proof: its outcome, summary, the section or reply it drafts for the pull request, its notes, a list of what
  it removed (for example "2 IP addresses"), and its screenshots, which go to upload links the server gives.

Your agent runs on your machine with your own model. GitRanks never sees your other files or your model's API key, and
your agent never gets your GitHub access. See the [privacy policy](https://gitranks.com/privacy) and the
[maintainers' page](https://gitranks.com/contribute/maintainers) for what GitRanks does with a change and how a
repository can opt out.

## License

MIT
