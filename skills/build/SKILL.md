---
name: build
description: Build a project on GitRanks Build, one small step at a time, with the code and the checks GitRanks gives. Use only when the user asks to build a project with GitRanks (for example "Teach me how to build an MCP server with GitRanks"), asks what they can build with GitRanks, asks to continue their GitRanks build, or says "continue my build" in a folder that has a .gitranks/build.json file. Not for building, compiling, running or fixing the user's own project or a failing build, and not for open-source issues. Needs the gitranks MCP server (https://mcp.gitranks.com/mcp).
---

# GitRanks Build

If the person did not name GitRanks or run `/gitranks-contribute:build`, and the folder has no `.gitranks/build.json`,
this skill does not apply: go on with what they asked as usual.

In GitRanks Build a person builds a real program from nothing with you, one small step at a time. GitRanks gives
each step: its code, what to show and tell the person, what to try, a check, and with questions on, a question. You
follow the step as it is written, and the person learns by reading it and trying it. They see every step, where they
stand and the tests on https://gitranks.com/build.

Each answer of the server is complete in itself and says exactly what to do. This skill is the frame around those
answers: keep to it in every step, even when an answer seems to leave room.

## When Build is not open

Build's tools on the `gitranks` server are `list_projects`, `open_build`, `next_step` and `reset_step`. Decide by
the tools you see:
- **No `gitranks` tools at all, or a call answers that sign-in is required:** the server is not connected. Connect it
  first (see Connecting in the `contribute` skill), then look again.
- **Other `gitranks` tools (such as `find_issues` or `my_contributions`) but none of Build's:** GitRanks Build is not
  open to this person yet. Tell them so, and do nothing more for GitRanks Build.

Never teach the project, write its code or make up its steps without the server.

## Start or continue

- **Which projects.** When the person asks what they can build, or wants to start one without naming it, call
  `list_projects` and let them pick.
- **Start.** If the folder's `.gitranks/build.json` names that project, continue that build instead (below). Else
  call `open_build` with `project` (its slug, such as `mcp-server`). The answer lists what to ask and run
  before the start: do those in order, one at a time, asking the person and waiting for each answer. Then call
  `open_build` again with the answers, as it says. Work only inside the build's folder from then on.
- **Continue.** When the folder has `.gitranks/build.json`, call `open_build` with its `build` as `buildId`. Else
  call `open_build` with nothing: it lists the person's builds in progress and what to ask.
- Keep the `buildId`: it continues the build in any chat and on any machine.
- **Questions on or off.** To change it later, call `open_build` with the `buildId` and `questions` (true or false).

## Each step

An answer that hands out a step has numbered parts. Do them in order, one at a time:

1. **Bring in the code exactly as given.** Run its commands as written, or write each file whole with exactly the
   text shown. Bring in only that code, and nothing else. Before you overwrite a file the person changed by hand (the
   step says how to tell), ask them and wait for their answer. Write `.gitranks/build.json` exactly as the step says.
   If the fetch fails, or you may not use the network, make the call the answer names for that, with `files: true`:
   it answers the files themselves.
2. **Show the person** exactly what the step shows.
3. **Say the step's text, adding no facts of your own.** Tell the person the text as the step gives it. Do not add
   examples, advice or facts, and do not drop any.
4. **Invite them to try** what the step lists, and let them.
5. **Run the check** with the exact command the step gives, and keep everything it prints.
6. **With questions on, ask the question and wait.** The person picks a letter. Never answer it for them and never
   hint at the right one.
7. **Call `next_step`** with the `buildId`, the step, the check text exactly as it was printed (all of it, even when
   it looks wrong) and, with questions on, the letter the person picked.

Then the answer is the next step, or the same step with what went wrong. If the person asks to explain more, read
them the text the step gives for that. If they ask something else, answer it, then come back to the step.

## What an answer may say

- **The build cannot start.** The language's runtime is missing or too old. Tell the person what to install, as the
  answer says, and start again once it is installed.
- **Git has no name and email.** Ask the person which name and email to use for this build's commits, and never take
  them from anywhere else. Then run the commands the answer gives, or go on with no git if the person prefers.
- **The check did not pass.** Tell the person what the answer says went wrong and follow its reasons, without writing
  code of your own. The check's command changes after a failure: run the new one from the answer and send what it
  prints. From the second failure the answer offers to set the step again with `reset_step`: offer it to the person.
- **The answer is not right.** Tell the person why, ask the question again and wait, then send the letter they pick
  with the same check text.
- **The whole step again, with no word that the check failed.** The step's code was corrected after it was handed
  out, so the check you sent ran on older code and was not judged. Tell the person what the answer says first, bring
  in the step's code again from part 1, run the check with the command in that answer and send what it prints.
- **An earlier step was corrected, or a step was added.** Tell the person the line the answer starts with. The step
  in hand brings the fix.
- **Not the step the build is on.** Go on with the step the answer gives.
- **The build was removed.** It was removed on gitranks.com and cannot go on: tell the person, and send nothing more
  for that `buildId`. To build the project again, ask them first, then start it again with `open_build` and
  `project`: it starts at step 1.
- **The base is done.** Give the person the link to the test. The test is taken on gitranks.com by the person alone:
  never answer it for them. The answer names the optional parts they can build next.
- **A part.** Open one with `open_build`, the `buildId` and `part`. One part at a time: when another part is in
  progress, that part goes on until it is built.
- **A refusal.** Tell the person in plain words what it says, then do what it says.

To set the folder back to a step the person passed, or to the step in hand (the files drifted, a check keeps
failing, or the person asks), call `reset_step` with the `buildId` and the step, and `files: true` when the fetch fails
or you may not use the network. It changes no progress and hands out no check. Then go on as its answer says.

## Rules

- Follow one step at a time. Never run ahead: no step before the server hands it out, and no part of a step before
  the part above it is done.
- Never write code of your own for a step, and never change the step's code to make a check pass.
- Send the check text exactly as it was printed. Never write it, edit it, or run the check on code other than the
  step's.
- Ask the person before you overwrite a file they changed.
- Never take a test, or answer a step's question, for the person.

## Help

Every step, where the person stands and the tests: https://gitranks.com/build. Questions: hello@gitranks.com.
