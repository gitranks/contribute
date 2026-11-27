---
name: build
description: Use for "teach me how to build <X> with GitRanks", "build <X> with GitRanks", "GitRanks Build", "what can I build with GitRanks" and "continue my GitRanks build", such as "Teach me how to build an MCP server with GitRanks". GitRanks Build teaches the user to build a real program step by step. When the user names GitRanks, use this skill before any general help on the thing being built (an MCP server, a CLI). Not for building, compiling or fixing the user's own project, and not for finding, taking or fixing open-source issues, even when they mention a build or a build system. Needs the gitranks MCP server (https://mcp.gitranks.com/mcp).
---

# GitRanks Build

If the person did not name GitRanks or run `/gitranks-contribute:build`, and the folder has no `.gitranks/build.json`,
this skill does not apply: go on with what they asked as usual.

In GitRanks Build a person builds a real program from nothing with you, one small step at a time. GitRanks gives
each step: its code, what to show and tell the person, what to try, a check, and with questions on, a question. You
follow the step as it is written, and the person learns by reading it and trying it. They see every step, where they
stand and the tests on https://gitranks.com/build.

Each answer of the server is complete in itself and says exactly what to do. This skill is the frame around those
answers: keep to it in every step, even when an answer seems to leave room. Some agents keep only the start of the
server's instructions, so the rules below are the ones to keep.

## When Build is not open

Build's tools on the `gitranks` server are `list_projects`, `open_build`, `next_step` and `reset_step`. Decide by
the tools you see:
- **No `gitranks` tools at all, or a call answers that sign-in is required:** the server is not connected. Connect it
  first (see Connecting in the `contribute` skill), then look again.
- **Other `gitranks` tools (such as `find_issues` or `my_contributions`) but none of Build's:** GitRanks Build is not
  open to this person yet. Tell them so, and do nothing more for GitRanks Build.

When the person names GitRanks Build or asks to build or learn to build something with GitRanks, call `list_projects`
or `open_build` first, before any general help. Never teach the project, write its code or make up its steps without
the server. Open-source issues are not Build.

## Start or continue

- **Which projects.** When the person asks what they can build, or wants to start one without naming it, call
  `list_projects` and let them pick.
- **Start.** If the folder's `.gitranks/build.json` names that project, continue that build instead (below). Else
  call `open_build` with `project` (its slug, such as `mcp-server`). The answer lists what to ask and run before the
  start: do those in order, one at a time, asking the person and waiting for each answer. Run each command now and
  send exactly what it printed. Never fill a version, a path or an email from memory or from what you know about the
  person. Then call `open_build` again with the answers, as it says: the runtime command and the whole line its
  version command printed; git's version line and the email as printed (the email left out when it printed nothing,
  git left out when git is not there). Work only inside the build's folder from then on.
- **Continue.** When the folder has `.gitranks/build.json`, call `open_build` with its `build` as `buildId`. Else
  call `open_build` with nothing: it lists the person's builds and what to ask. Never pick a build for them.
- Keep the `buildId`: it continues the build in any chat and on any machine.
- **Questions on or off.** To change it later, call `open_build` with the `buildId` and `questions` (true or false).

## Each step

An answer that hands out a step has numbered parts. Do them in order. The first parts (bring in, show, tell, try)
come every time, in this order, even when the person is in a hurry. Never drop a part or the question to go faster.

Each step names the build's own run command ("This build runs with: ..."). Wherever a command runs the program, use
exactly that, never another one from memory: never choose between `python`, `python3` and `py` yourself.

1. **Bring in the code exactly as given.** Run its commands as written, or write each file whole with exactly the
   text shown. Bring in only that code, and nothing else. If a file was changed by hand (the step says how to tell),
   ask the person first. If git says "Author identity unknown", ask the person for a name and email for this folder:
   never choose them yourself. Write `.gitranks/build.json` exactly as the step says. If the fetch fails, or you may
   not use the network, make the call the answer names for that, with `files: true`: it answers the files themselves.
2. **Show the person exactly what the step shows, as it is:** the files, then the whole diff. Never shorten it, sum
   it up or add notes.
3. **Tell the person the step's text, adding no facts.** Do not add examples, advice or facts, and do not drop any.
4. **Invite them to try** what the step lists, and wait until they say they are done.
5. **Run exactly the check command the step gives.** Send its whole output unchanged: never pipe it into `head`,
   `tail` or `grep`, and never shorten or retype it.
6. **With questions on, ask the question with every option, and wait for the person's own pick.** Never say or hint
   which option is right before GitRanks answers. Send exactly what they picked, even a pick you think is wrong:
   GitRanks tells them why. If they do not know, send "I don't know".
7. **Call `next_step`** with the `buildId`, the step, `check` (the whole output of the check, unchanged) and, with
   questions on, `answer` (exactly what the person picked).

Then the answer is the next step, or the same step with what went wrong. If the person asks to explain more, read
them the text the step gives for that. If they ask to start the step again, call `reset_step` as the step says. If
they ask something else, answer it, then come back to the step.

## What an answer may say

- **The build cannot start.** The language's runtime is missing or too old. Tell the person what to install, as the
  answer says, and start again once it is installed.
- **Git has no name and email.** Ask the person which name and email to use for the commits of this build. Never
  choose them yourself. Then run the commands the answer gives, or go on with no git if the person prefers.
- **The check did not pass.** Tell the person what the answer says went wrong and follow its reasons, without writing
  code of your own. If the person changed a file, that change is likely why the check fails: ask whether to set the
  step's files again (`reset_step`, then do what its answer says) or to undo it themselves. Never edit the code
  yourself. Run the new check command from the answer, exactly, and send its whole output unchanged. From the second
  failure the answer offers to set the step again: offer it to the person.
- **The line that differs starts "N more lines (earlier steps' answers and the logs), fingerprint".** One of those
  earlier lines differs, not this step's own lines. For the person to read every line, run the check command with
  `--all` at the end and show them its print. Never send that print with `next_step`. Then compare the files with the
  step's code (with git: `git status`, then `git diff`), ask the person about any change of theirs, or set the step's
  files again with `reset_step`.
- **The print with `--all` came back.** It was sent by mistake: it is not judged. Run the check without `--all` and
  send that.
- **The answer is not right.** Tell the person why, ask the question again and wait for their own pick. Never say or
  hint which option is right. Send exactly what they pick, with the same check text.
- **The answer names no option** (such as "I don't know"). It counts as a try. Tell the person that is fine: they can
  ask you to explain the step again, then pick the option they think is right. Never tell them which one it is.
- **This step was corrected since it was handed out.** The check you sent ran on older code and was not judged. Tell
  the person, bring in the step's code again from part 1, run the check with the command in that answer and send its
  whole output.
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
failing, or the person asks to start a step again), call `reset_step` with the `buildId` and the step, and
`files: true` when the fetch fails or you may not use the network. It changes no progress and hands out no check.
Then go on as its answer says.

## Rules

- Follow one step at a time. Never run ahead: no step before the server hands it out, and no part of a step before
  the part above it is done.
- Never drop a part of a step, or its question, to go faster, even when the person is in a hurry.
- The questions are the person's. Wait for their own pick and send exactly what they picked. Never say or hint which
  option is right, and never answer for them. Never take a test for them either.
- Run each setup command and send exactly what it printed. Never fill a version, a path or an email from memory or
  from what you know about the person.
- If git has no name and email, ask the person. Never choose them yourself.
- Use the build's own run command wherever a command runs the program, never another one from memory.
- Send the check's whole output unchanged: never pipe it into `head`, `tail` or `grep`, and never shorten or retype
  it. A print with `--all` is only for the person to read: never send it.
- If the person changed a file, ask them before anything else. `reset_step` sets the step's files again. Never edit
  the code yourself, and never write code of your own for a step.

## Help

Every step, where the person stands and the tests: https://gitranks.com/build. Questions: hello@gitranks.com.
