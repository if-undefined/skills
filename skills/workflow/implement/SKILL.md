---
name: implement
description: Implement a change through to a pull request. Use when the user's request says "implement".
---

# Implement

1. **Branch.** When HEAD is already this work's branch, stay on it; its base is the open PR's base, else the base chosen below. Otherwise choose a base and branch from it:
   - Base: the remote default branch (`origin/<default>`) after a fetch, unless this work builds on commits that exist only on another unmerged branch (a **Blocked by** ticket's branch, or the branch checked out now). Then base on that branch.
   - Create: `git switch --no-track -c <name> <base>`; `--no-track` keeps a remote base from becoming the push target. Name it from the ticket id plus a short kebab slug when a ticket exists (e.g. `42-add-login`); otherwise a kebab slug from the change intent. Earlier work arrives only through the base.
   - Done when: HEAD is on this work's branch, its name matches that pattern, and `git merge-base --is-ancestor <base> HEAD` succeeds (a read-only check that HEAD contains every commit on the base).

2. **Build.** Implement against the tickets or spec until their acceptance criteria are met. Prefer the narrowest change that satisfies them. When neither is present, implement the user's ask the same way.
   - Done when: every acceptance criterion (or stated ask) is satisfied (or explicitly deferred by the user).

3. **Prove.** Get proof for every behavior the diff changes and every refactor. Proof is evidence you observed yourself in this session. Use the first option you can carry out:
   1. For a fix, reproduce the original failure against the base, then run the same reproduction against the change.
   2. For a behavior with no test, in a project with a test setup, add one focused test. Watch it fail on the base and pass on the change.
   3. For UI, run the app and look at the change.
   4. For a refactor or any other change, run the project's checks that cover the changed code. Find the checks in the environment, such as package scripts, a Makefile or the CI config.
   5. If you can carry out none of these, record an open check for the PR's test plan.

   **Trace criteria.** Map each acceptance criterion to the test, file, or behavior that proves it. A fixture or artifact a ticket names must be the real one. Fix each unmapped criterion or report it as deferred. When the ticket file tracks status, tick the criteria and update its status.
   - Done when: every changed behavior and refactor has proof or an open check, every check you ran passes, every criterion is mapped or reported as deferred, and the ticket reflects the result.

4. **Commit.** Commit the proved changes with the `/commit` skill, and use `/commit` for every commit.
   - Done when: `git status` shows a clean tree for the intended work.

5. **Review.** Dispatch a subagent to run the `/review` skill on this branch. Give it the base from step 1, and the ticket or spec path, else the user's ask verbatim. When earlier reviews exist, from this run or an earlier one, also give it the latest report and every finding declined so far, each with its reason.

   Answer every finding in the report. Fix each one you agree with by the narrowest change, proved and committed through steps 3 and 4. Decline the rest, each with a one-line reason and its evidence, such as a `path:line`, a test or command output. After a review that led to a fix, dispatch a follow-up review the same way, up to three reviews per run.
   - Done when: every finding is fixed or declined, and the run's last review led to no fix or was its third.

6. **PR.** Open or update the pull request with the `/to-pr` skill, against the base from step 1, and use `/to-pr` for every PR you create or edit. Give it each open check from step 3 for the test plan, and a review report for a `## Review` heading in the body. The report opens with the last review's mode, reviewed commit, base and intent's source. Then comes a table of every finding declined so far that `HEAD` still has, with the review table's columns plus a Reason column. With no declined finding left, the report says "No open findings" in place of the table.
   - Done when: `/to-pr` has returned the PR URL, and the PR body has every open check in its test plan and the review report under `## Review`.
