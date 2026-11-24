---
description: Find open-source GitHub issues matched to your skills on GitRanks Contribute, and start on the one you choose
argument-hint: "[language, kind or owner/repo]"
---

Use the `contribute` skill. Call `find_issues` with the filters the user gave in $ARGUMENTS (a language, a kind of
issue, or an `owner/repo`), or none. Issue details are hidden until an issue is taken: show the first few issues by
what each item gives (its title, language, kind, size, the project's tier and hints). Ask which one to take, unless the
user named one, then follow the skill's loop from step 2: call `claim_issue` with the one they pick, by its
`masked.id` as `maskId`, or by its `issueId` when its `masked` is null.
If none come back, say so as the skill's Find step does: fewer filters, or what to widen.
