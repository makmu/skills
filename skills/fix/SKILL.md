---
name: fix
description: Use when the user asks to fix, resolve, or implement a GitHub issue. Determines the issue number, implements the fix, and opens a pull request that links the issue.
---

# Fix a GitHub issue

## 1. Get the issue number

An issue number is required.

- If the user provided one (e.g. "fix #88", "fix issue 88"), use it.
- Otherwise, ask the user for the issue number before doing anything else. Do not guess, and do not pick an arbitrary open issue.

Then fetch the issue to understand what is being asked:

```sh
gh issue view <number>
```

Read the issue title, body, and any comments. If the requirements are ambiguous, ask the user for clarification before implementing.

## 2. Implement the fix

- Create a branch for the fix; do not commit to the default branch.
- Investigate the relevant code before changing it, and keep the change consistent with the surrounding structure, naming, and style.
- Consult the project's architecture and UX guidelines when the task requires it.
- Add or adjust tests where the project does so for comparable changes.
- Verify the change (build, tests, linters) before committing.

## 3. Commit

Commit messages for issue fixes must start with the issue number, followed by a colon and the actual message:

```
#88: Fix wrong event date on the homepage
```

## 4. Create the pull request

Push the branch and open the PR with the `gh` CLI:

```sh
gh pr create
```

The PR must:

- Start its description with a closing keyword linking the issue, e.g. `Closes #88` (`Fixes #88` or `Resolves #88` also work). Only omit this if the user explicitly says not to.
- Summarize what changed and why, and note how it was verified.

## 5. After the PR

- Do **not** close the issue yourself. Merging the PR closes it via the closing keyword. Never close an issue without explicit confirmation from the user.
- Report the PR URL back to the user.
