---
description: Build a real program step by step with GitRanks Build, or continue your GitRanks build
argument-hint: "[project]"
---

Use the `build` skill. If you see no tools of the `gitranks` server, or a call answers that sign-in is required,
connect it first, as the skill says. If GitRanks Build is not open to the user (see the skill), say so and stop.

If the user named a project in $ARGUMENTS and the folder's `.gitranks/build.json` names that project, call
`open_build` with its `build` as `buildId`. Else, if they named a project, call `list_projects` to find its slug
(unless they gave the slug, such as `mcp-server`), then call `open_build` with it as `project`. With no project
named: when the folder has `.gitranks/build.json`, call `open_build` with its `build` as `buildId`; else call
`open_build` with nothing, which lists the user's builds in progress and what to ask. Then follow the answer and the
skill, one step at a time.
