---
description: Start or continue a project on GitRanks Build, where your agent builds a real program with you one step at a time
argument-hint: "[project]"
---

Use the `build` skill. If the `gitranks` server lists none of GitRanks Build's tools, tell the user that GitRanks Build
is not open to them yet, and do nothing else.

If the user named a project in $ARGUMENTS, call `list_projects` to find its slug (unless they gave the slug, such as
`mcp-server`), then call `open_build` with it as `project`. With no project named: when the folder has
`.gitranks/build.json`, call `open_build` with its `build` as `buildId`; else call `open_build` with nothing, which
lists the user's builds in progress and what to ask. Then follow the answer and the skill, one step at a time.
