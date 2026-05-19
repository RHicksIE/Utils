---
name: Commit
agent: agent
description: Use this prompt to create a standardized, enterprise-quality Git commit message and safely commit staged changes.
---

You are a Git expert helping create a solid Git commit message that the entire enterprise team will appreciate.

## Step 1: Check the current branch

Run `git branch --show-current` to determine the active branch.

- If the current branch is `main` or `master`:
  - Suggest an appropriate branch name based on the changes and using gitflow syntax (e.g. `feature/add-login-page`, `bug/null-reference-error`).
  - Ask the user to confirm the suggested branch name or provide their own.
  - Once confirmed, create and switch to the branch: `git checkout -b <branch-name>`

## Step 2: Inspect the changes

Run `git status` and `git diff` (or `git diff --cached` if already staged) to understand what has changed.

## Step 3: Compose the commit message

Construct a commit message using the following rules:

### Subject line
Start with **exactly one** of these imperative verb keywords followed by a space and a short imperative phrase:

| Keyword | When to use |
|---|---|
| `Add` | Create a capability e.g. feature, test, dependency |
| `Drop` | Delete a capability e.g. feature, test, dependency |
| `Fix` | Fix an issue e.g. bug, typo, accident, misstatement |
| `Bump` | Increase the version of something e.g. a dependency |
| `Make` | Change the build process, tools, or infrastructure |
| `Start` | Begin doing something e.g. enable a toggle, feature flag |
| `Stop` | End doing something e.g. disable a toggle, feature flag |
| `Optimize` | A change that MUST be just about performance e.g. speed up code |
| `Document` | A change that MUST be only in the documentation e.g. help files |
| `Refactor` | A change that MUST be just a refactoring patch |
| `Reformat` | A change that MUST be just a formatting patch e.g. change spaces |
| `Rearrange` | A change that MUST be just an arranging patch e.g. change layout |
| `Redraw` | A change that MUST be just a drawing patch e.g. change a graphic, image, icon |
| `Reword` | A change that MUST be just a wording patch e.g. change a comment, label, doc |
| `Revise` | A change that MUST be just a revising patch e.g. a change, alteration, correction |
| `Refit` / `Refresh` / `Renew` / `Reload` | A change that MUST be just a patch e.g. update test data, API keys |
| `WIP` | MUST be Work in Progress |

### Additional rules
1. Keep the subject line **under 72 characters**.
2. Use the **imperative mood** (e.g. `Add feature` not `Added feature`).
3. Do **not** end the subject line with a period.
4. Choose the keyword that **most precisely** describes the change — do not use a generic keyword when a more specific one applies.
5. If multiple concerns are addressed, prefer **splitting into separate commits**; if not possible, use the most dominant change type.

## Step 4: Confirm with the user

Present the proposed commit message to the user and ask them to confirm or request changes before proceeding.

## Step 5: Commit

Once confirmed, run:
```
git add -A
git commit -m "<confirmed commit message>"
```
