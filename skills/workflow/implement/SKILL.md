---
name: implement
description: Implement a change through to a pull request. Use when the user's request says "implement".
---

# Implement

## Steps

1. **Branch** from this work's base, or stay on this work's branch.
2. **Build** the change, proving each behavior it changes.
3. **Verify** with the project's checks, and trace every acceptance criterion.
4. **Commit** the proved changes with the `/commit` skill, and use `/commit` for every commit. Done when `git status` shows a clean tree for the intended work.
5. **Review** the branch with `/review` in a subagent, fixing or declining every finding.
6. **PR**: open or update the pull request with the `/to-pr` skill.

## Branch

When HEAD is already this work's branch, stay on it; its base is the open PR's base, else the base chosen below. Otherwise choose a base and branch from it:

- **Base**: the remote default branch (`origin/<default>`) after a fetch, unless this work builds on commits that exist only on another unmerged branch (a **Blocked by** ticket's branch, or the branch checked out now). Then base on that branch.
- **Create**: `git switch --no-track -c <name> <base>`; `--no-track` keeps a remote base from becoming the push target. Name it from the ticket id plus a short kebab slug when a ticket exists (e.g. `42-add-login`); otherwise a kebab slug from the change intent. Earlier work arrives only through the base.

Done when: HEAD is on this work's branch, its name matches that pattern, and `git merge-base --is-ancestor <base> HEAD` succeeds (a read-only check that HEAD contains every commit on the base).

## Build

Implement against the tickets or spec until their acceptance criteria are met. Prefer the narrowest change that satisfies them. When neither is present, implement the user's ask the same way.

Prove each behavior you change and each refactor as you make it. Exercise it the way its consumers use it, make the change, exercise it again, and compare the results with what the ticket, ask or review finding requires. Proof is evidence you observed yourself in this session. Keep each proof as a test when the project's test setup can express it. For a change that already exists, get the earlier result from a temporary worktree at the last commit without it. Record what you cannot prove as an open check for the PR's test plan.

Done when: every acceptance criterion, or each part of the stated ask, is satisfied or deferred with the reason it cannot be met, and every changed behavior and refactor has earlier and later results that match what is required, or an open check.

## Verify

Run the project's checks that cover the changed code. A check that fails the same way in a temporary worktree at the last commit gets an open check.

**Trace criteria.** Map each acceptance criterion to the test, file, or behavior that proves it. A fixture or artifact a ticket names must be the real one. Fix each unmapped criterion or defer it as in Build. When the ticket file tracks status, tick the criteria and update its status.

Done when: every project check that covers the changed code has run and passes or has an open check, every criterion is mapped or deferred, and the ticket reflects the result.

## Review

Dispatch a subagent to run the `/review` skill on this branch. Give it the base from Branch, and the ticket or spec path, else the user's ask verbatim. When this run has an earlier review, or the open PR has a `## Review` section, also give it the latest report and every finding declined so far, each with its reason.

Answer every finding in the report. Fix each one you agree with by the narrowest change, built, proved and committed through Build, Verify and Commit. Decline the rest, each with a one-line reason and its evidence, such as a `path:line`, a test or command output. After a review that led to a fix, dispatch a follow-up review the same way, up to three reviews per run.

Done when: a review has returned its report, every finding is fixed or declined, and the run's last review led to no fix or was its third.

## PR

Open or update the pull request with the `/to-pr` skill, against the base from Branch, and use `/to-pr` for every PR you create or edit. Give it each open check from Build and Verify and each deferral with its reason for the test plan, and a review report for a `## Review` heading in the body.

The report opens with the last review's mode, reviewed commit, base and intent's source. Then comes a table of every finding declined so far that `HEAD` still has, with the review table's columns plus a Reason column. With no declined finding left, the report says "No open findings" in place of the table.

Done when: `/to-pr` has returned the PR URL, and the PR body has every open check and deferral in its test plan, and the review report under `## Review`.
