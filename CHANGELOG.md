# Changelog

## Unreleased

## 0.6.0 (2026-11-27)

- GitRanks Build is not open to everyone yet: it opens step by step. When it is open to you, a new `build` skill
  and the command `/gitranks-contribute:build [project]` start or continue a project on GitRanks Build, where your
  agent builds a real program with you one step at a time. The skill keeps your agent to each step as GitRanks gives
  it: it brings in only the code given, says the step's text adding no facts, runs the check and sends what it
  printed, asks you before it overwrites a file you changed, and never runs ahead or writes code of its own. The
  skill is written to load only when you ask to build a project with GitRanks, not when you build your own project.
  When GitRanks Build is not open to you yet, your agent says so and goes on with anything else you asked.
- "What is sent to GitRanks" in the README names what GitRanks Build sends.

## 0.5.1 (2026-11-26)

- The long description in `plugin.json` (`interface.longDescription`) opens with "GitRanks Contribute finds open-source
  GitHub issues that fit your skills".

## 0.5.0 (2026-11-25)

- Before an agent takes its first issue, the user finishes a 2-minute setup on gitranks.com once: it shows how
  approval works, what the agent may do and the daily limits. The skill says: if an answer says setup is not
  finished, give the user the link it names and take no issue until they are done (when connecting, when taking an
  issue, and in GitRanks Learn). A `setup_unfinished` refusal takes none of the day's full issues.
- The README opens with what happens: your agent fixes open-source issues picked for you, and you approve each pull
  request on gitranks.com. New parts: the install buttons up top, "How it works", "Before your agent takes its first
  issue" (with the setup link), "Learn while you fix" and "Your GitRanks pages". "How you connect" is now the first
  part of "Install", and the README and `llms-install.md` point to Your agent on gitranks.com for connected agents
  and personal tokens. The skill's link for widening languages or kinds goes to the Settings page itself.
- New description in every manifest: "Your agent fixes open-source issues picked for you. You approve every pull
  request on gitranks.com." Devin's short description is "Fix picked open-source issues".
- The README and the skill no longer speak of autopilot, which GitRanks does not have yet: nothing reaches GitHub
  before the user approves the pull request on gitranks.com.

## 0.4.4 (2026-11-24)

- GitRanks Learn: Learn mode lists the issues the user's Learn Issues page shows For you, from their Learn languages
  and level; the skill no longer speaks of a Learn goal.

## 0.4.3 (2026-11-24)

- GitRanks Learn: the skill says a lesson has 3 to 5 steps, as the lesson's brief now asks.

## 0.4.2 (2026-11-24)

- The README no longer calls GitRanks Contribute a beta.
- GitRanks Learn: open to everyone, so the skill no longer says what to do when Learn is not open to the user.

## 0.4.1 (2026-11-24)

- GitRanks Learn: each item `find_issues` lists in Learn mode also gives `lesson`, the course lesson the issue teaches
  or null, and `lessonWhy` (`uses_learned`, `teaches_new` or `no_lesson`); a Learn claim's answer adds `lesson`.
  `submit_lesson` takes `courseLesson`, the slug of the one lesson the change used or null, when the `lessonBrief`
  lists the issue's lessons (one it did not list answers `unknown_lesson`). The skill says so.
- "What is sent to GitRanks" in the README now names a follow-up's verdict on each failing check, what the agent
  says only you can do next, and which course lesson a Learn fix used.
- The skill stops saying "claim" to the user in three more places (the issue it took, an issue no longer held after
  the fifth failed submission, an agent with no shell), and the plugin's release notes say "take".

## 0.4.0 (2026-11-24)

- Issue details are hidden until an issue is taken. `find_issues` lists masked issues: a rewritten title, the
  language, the kind, the size, the project's tier and hints, with no repository or link. The skill and
  `/gitranks-contribute:find` show those and take the issue the user picks by its `masked.id` (`claim_issue`'s
  `maskId`).
- Each issue taken counts against the user's full issues a day: 10 to 70 by their GitRanks tier, plus 5 for each pull
  request merged through GitRanks, up to 100. An issue the user holds open on gitranks.com is taken at no new cost.
- When the agent talks to the user, it says they take an issue. `/gitranks-contribute:status` lists the issues the
  user took.
- `release_issue`: the skill names the reasons. A fixed, closed, taken, turned-down or outdated issue is read again on
  GitHub and taken out for everyone if it is no longer open; any other reason gives it back to others.
- The GitRanks rule in the skill, word for word as the server's: each issue taken counts against the user's full
  issues a day, and a pull request opened outside GitRanks for an issue taken here, or many issues taken with few pull
  requests through GitRanks, brings a message, then 5 full issues a day, then access to real issues closed. It no longer speaks
  of shown issues or a shorter list.

## 0.3.6 (2026-11-22)

- The skill's rules start with the GitRanks rule for issues from the user's list, word for word as the server's
  instructions give it: only GitRanks opens the pull request, so the agent never pushes a branch, forks the repository
  or opens the pull request itself (for example with `gh pr create`), and sends the patch with `submit_patch`. If the
  user asks it to open the pull request itself, it says the rules do not allow that and offers `release_issue`. The
  list belongs to GitRanks: the agent does not save, export or pass it on. A pull request opened outside GitRanks
  brings a message first, then a shorter list, then a blocked account.

## 0.3.5 (2026-11-18)

- GitRanks Learn: the skill no longer calls Learn invite-only, says when to use Learn mode and what to tell the user
  on `learn_closed`.
- GitRanks Learn: when the user asks to fix an issue URL "with GitRanks Learn" (the prompt gitranks.com gives for the
  issue they picked), the skill claims that URL in Learn mode and follows the Learn steps.

## 0.3.4 (2026-11-18)

- The skill links the language filters where they are, on the settings page.

## 0.3.3 (2026-11-18)

- After each step the skill tells the user what happened and what comes next: what was claimed and until when, why a
  claim or an issue was given back, and the review link after `submit_patch` (unless autopilot is on, nothing reaches GitHub
  before the user approves). It also covers an empty list, a refused claim and a send-back, and ends with where to get help.
- `/gitranks-contribute:find` and `/gitranks-contribute:status` say what to do when nothing comes back.
- The README says what to ask your agent once signed in, what happens at the approval, and links the MCP docs; the
  Claude Desktop and claude.ai section says the fix needs an agent with a shell.

## 0.3.2 (2026-11-17)

- On a follow-up, the skill says to fix only the failing checks the pull request's change causes, and to report
  whose each failing check is: `checks` on `submit_patch` or `release_issue`.

## 0.3.1 (2026-11-16)

- The README has a Support section: email, issues and the FAQ.
- A security policy (`SECURITY.md`): report issues privately by email.
- The Devin manifest follows the Devin marketplace's style: a short description of 40 characters or fewer, and no
  period at the end of the description.

## 0.3.0 (2026-11-15)

- Ready for the plugin directory shared by ChatGPT and Codex: the root `plugin.json` has the listing (a 30-character
  subtitle, a longer description that says the fix needs an agent with a shell, capabilities, a support page and three
  starter prompts), the review's test cases and demo video, and the release notes. `mcp.json` says the server signs in
  with OAuth and registers its client itself.
- The README has ChatGPT's setup: add a custom MCP server with the URL and OAuth, then sign in on gitranks.com. In
  ChatGPT you find, claim and track issues; the fix needs Codex or another agent with a shell.
- The skill says what to do without a shell: find, claim and track, and say the fix needs an agent with a shell (or
  give the issue back). For signing in again it names apps such as ChatGPT too.
- The server has a prompt, **Find an open-source issue for me** (`find_issue`): clients that list prompts show it as a
  command or menu item, so you can start without typing the request. "Use it" says so.
- The README opens with a short clip of the Claude Code setup: install the plugin, sign in once, ask for an issue.

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
