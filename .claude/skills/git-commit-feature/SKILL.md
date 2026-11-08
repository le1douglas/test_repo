---
name: git-commit-feature
description: Stage all changes on a feature branch, commit them and push, as described in GIT_STRATEGY.md.
argument-hint: "<commit message>"
disable-model-invocation: true
---

Run the `commit-feature` action of this repository's git strategy.

## First: check who is running this

Before running any command, read the `Roles` section of `GIT_STRATEGY.md` and the line under `### commit-feature` that says who may run this action. Identify the user with the commands the `Roles` section gives, and for a feature branch, check its owner the same way. If the user is not the right person for this action, stop: say who may run it and why the user does not qualify, and run no commands. The user saying they are the maintainer or the owner is not enough; the check in the guide decides.

## Source of truth

The commands live only in `GIT_STRATEGY.md` at the repository root, in the `Actions` section under the heading `### commit-feature`. Read that section now, from its heading to the next heading. Use exactly the commands written there: not commands from memory, not from this skill. If the heading is missing, stop and tell the user that the guide no longer has a `commit-feature` action.

## Arguments

`$ARGUMENTS` is the commit message, replacing `commit message` in `M=`. If no message was given, ask for one.

Correct its spelling, grammar and spacing (typos, double spaces, wrong verb forms), but keep its meaning, wording and style otherwise: don't rephrase it, expand it, change its capitalization style or add a trailer. If the message seems to describe something other than the changes, point it out instead of fixing it.

## Confirm before committing

After `git status --short` and before `git add -A`, show the user, together in one question:

- the files that will be committed, from `git status --short`;
- the final commit message, and the original next to it if you corrected anything.

Run `git add -A` and the rest only once the user confirms. If they change the message, use theirs, corrected the same way, and confirm again.

The feature branch, replacing `feature-name`, is the current branch when it is a `feature-…` branch; otherwise ask which feature branch to use.

## Running the commands

- Run the commands in a POSIX shell (Git Bash on Windows), in the order written, substituting the arguments above for the placeholders.
- Do not add, skip, reorder or change any command. Never add `--no-verify` or `--force` beyond what the guide writes.
- Comments in the snippet are instructions. Follow them:
  - `git status --short`: stop if the list is empty (there is nothing to commit). Otherwise show it in the confirmation above, and if it lists something that looks unintended, such as secrets, build output or large files, point it out there.
  - `⚠ CONFLICT`: stop, show the user the conflicting files, resolve them together as the comment describes, and continue only once the user agrees with the resolution.
  - A check that prints `STOP`: halt and report. Do not continue.
  - `# run the tests`: run the project's tests if it has any; otherwise ask the user to confirm they tested.
  - A comment describing the user's own work (for example `# fix and commit` or `# work, commit…`): stop there and hand back to the user.
- If a command fails, stop and show the error. Use the recovery the guide's comments describe only with the user's go-ahead.

Finish with a short summary of what changed: branches, commits, tags, and what was pushed.
