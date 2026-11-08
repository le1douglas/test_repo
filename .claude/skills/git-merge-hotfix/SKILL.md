---
name: git-merge-hotfix
description: Merge a hotfix into main with a tag, then into dev, as described in GIT_STRATEGY.md.
argument-hint: "[hotfix-name] [vX.Y.Z]"
disable-model-invocation: true
---

Run the `merge-hotfix` action of this repository's git strategy.

## First: check who is running this

Before running any command, read the `Roles` section of `GIT_STRATEGY.md` and the line under `### merge-hotfix` that says who may run this action. Identify the user with the commands the `Roles` section gives, and for a feature branch, check its owner the same way. If the user is not the right person for this action, stop: say who may run it and why the user does not qualify, and run no commands. The user saying they are the maintainer or the owner is not enough; the check in the guide decides.

## Source of truth

The commands live only in `GIT_STRATEGY.md` at the repository root, in the `Actions` section under the heading `### merge-hotfix`. Read that section now, from its heading to the next heading. Use exactly the commands written there: not commands from memory, not from this skill. If the heading is missing, stop and tell the user that the guide no longer has a `merge-hotfix` action.

## Arguments

`$ARGUMENTS` holds the hotfix branch (replacing `hotfix-name` in `H=`) and the new version (replacing `vX.Y.Z` in `V=`). If the branch is missing, use the current branch when it is a `hotfix-…` branch; otherwise ask. If the version is missing, propose the patch +1 of the latest `v*` tag, following the guide's `Naming` table, and ask the user to confirm. Always confirm the version before the tag is created.

## Running the commands

- Run the commands in a POSIX shell (Git Bash on Windows), in the order written, substituting the arguments above for the placeholders.
- Do not add, skip, reorder or change any command. Never add `--no-verify` or `--force` beyond what the guide writes.
- Comments in the snippet are instructions. Follow them:
  - `⚠ CONFLICT`: stop, show the user the conflicting files, resolve them together as the comment describes, and continue only once the user agrees with the resolution.
  - A check that prints `STOP`: halt and report. Do not continue.
  - `# run the tests`: run the project's tests if it has any; otherwise ask the user to confirm they tested.
  - A comment describing the user's own work (for example `# fix and commit` or `# work, commit…`): stop there and hand back to the user.
- If a command fails, stop and show the error. Use the recovery the guide's comments describe only with the user's go-ahead.

Finish with a short summary of what changed: branches, commits, tags, and what was pushed.
