# Changelog

## 0.2.6 (2026-11-14)

- Antigravity signs in like the other clients: add the server with the URL alone, then, in the agent's window, click
  **Customizations**, scroll down to **MCP servers** and click **Sign in** next to `gitranks`. The **Authenticate**
  button on the **Manage MCP Servers** page doesn't sign in. A token still works, as in "Use a token instead".
- The Antigravity token setup restarts the server from the agent window's **Customizations**, not from Settings.

## 0.2.5 (2026-11-14)

- The Gemini CLI extension signs in only, like the Claude plugin: its optional token setting and the
  `X-GitRanks-Token` header are gone. If you set a token there, run `/mcp auth gitranks` after updating, or add the
  server with a token as in "Use a token instead".
- "Use a token instead" no longer reads the token from an environment variable: the Codex, Cursor and Gemini CLI
  examples take the token itself.

## 0.2.4 (2026-11-14)

- New description in every manifest and at the top of the README: "Find open-source GitHub issues matched to your
  skills", with `contribute`, `github-issues`, `pull-request`, `help-wanted` and `first-contribution` as keywords. The
  skill's trigger and the `/gitranks-contribute:find` description name GitHub issues too.
- The skill has GitRanks Learn's steps (invite-only): `find_issues` and `claim_issue` with `mode: "learn"`, one commit
  for `submit_patch`, then `submit_lesson` with the lesson on the fix. "What is sent to GitRanks" names the lesson.

## 0.2.3 (2026-11-13)

- The Claude plugin signs in only: its optional token setting and the `X-GitRanks-Token` header are gone, so the
  plugin's server now loads in Cowork too (Cowork skips a server whose setting has no default). A token in Claude Code
  now goes through `claude mcp add --header` (see "Use a token instead").
- If you set a token in the Claude plugin: after updating, run `/mcp`, pick `plugin:gitranks-contribute:gitranks` and
  choose **Authenticate** to sign in, or keep the token with the `claude mcp add --header` line in "Use a token instead".
- The README has a Codex and a Cursor section: what the agent does, on your own plan, step by step, and a
  "Fair to maintainers" section with the limits every client shares. The Cursor setup moved out of the old
  "Cursor, VS Code and Kiro" section, now "VS Code and Kiro".

## 0.2.2 (2026-11-12)

- One-click install links at the top of the README for claude.ai and Claude Desktop, Cursor, VS Code and Kiro.
- The README's Claude Desktop and claude.ai path is now Customize → Connectors → Add → Add custom connector.
- The README gives the one-line Claude Code plugin install for Claude Code 2.1.292 and later.
- Setup lines with their sign-in step for GitHub Copilot CLI, Devin, Kiro, Amp, opencode, Zed, Cline, Factory droid,
  Warp, and the `mcp-remote` bridge for clients without sign-in for remote servers (JetBrains AI Assistant, Augment).
- Codex plugin marketplace at `.agents/plugins/marketplace.json`, and the plugin's name, description, links and icon
  for Codex and ChatGPT in the root `plugin.json`.
- Devin plugin manifest at `.devin-plugin/plugin.json`, with the server by its URL alone.
- Antigravity plugin manifest at `.antigravity-plugin/plugin.json`, with its server in `mcp_config.json` (sign-in; not
  tested in Antigravity yet).
- The README lists the plugin formats in the repository, and its gitranks.com links carry UTM tags.

## 0.2.1 (2026-11-11)

- `llms-install.md` points agents to gitranks.com/contribute/agents.md.
- The skill says how the server connects: the user signs in on gitranks.com (with the sign-in step for Claude Code,
  Gemini CLI and Codex), and a token is only for clients that can't sign in.

## 0.2.0 (2026-11-11)

- Sign in instead of copying a token: the Claude Code plugin and the Gemini CLI extension connect with the URL alone,
  and your agent opens gitranks.com in the browser to sign in.
- The token is optional, for clients without sign-in. When set, it goes in the `X-GitRanks-Token` header instead of
  `Authorization`.
- Agent Plugins `plugin.json` and `mcp.json` at the root, for clients and marketplaces that install that format.
- VS Code setup in the README.
- The README and `llms-install.md` set up each client by URL and sign-in, keep a "Use a token instead" section, and say
  what signing in sends to GitRanks.
- The README says every pull request opened from gitranks.com names GitRanks Contribute and your agent.
- Antigravity setup in the README.
- Claude Code commands `/gitranks-contribute:find` and `/gitranks-contribute:status`.
- The skill follows the server: the 48-hour lapse without a passing patch, never posting on GitHub, and proofs.
- The README names everything sent, including the agent's name and model, the suggested pull request text and proofs.

## 0.1.0 (2026-11-03)

- Claude Code plugin and marketplace, Gemini CLI extension, and the `contribute` skill for the GitRanks Contribute MCP
  server at `https://mcp.gitranks.com/mcp`.
