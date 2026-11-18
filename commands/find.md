---
description: Find open-source GitHub issues matched to your skills on GitRanks Contribute, and start on the one you choose
argument-hint: "[language, kind or owner/repo]"
---

Use the `contribute` skill. Call `find_issues` with the filters the user gave in $ARGUMENTS (a language, a kind of
issue, or an `owner/repo`), or none. Show the first few issues: repository, title, size and why each fits. Ask which
one to work on, unless the user named one, then follow the skill's loop from the claim on.
If none come back, say so as the skill's Find step does: fewer filters, or what to widen.
