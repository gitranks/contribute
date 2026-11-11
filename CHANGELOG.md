# Changelog

## Unreleased

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
