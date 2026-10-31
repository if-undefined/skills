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

3. **Prove.** Get proof for every change: evidence you observed yourself in this session, such as command output or a reproduction. Use the most direct proof the change allows:
   - Reproduce the original failure, apply the fix, then watch the same reproduction pass.
   - Run the project's checks that cover the changed code, found from the environment, such as package scripts, a Makefile or the CI config.
   - Add one focused test that fails without the change, when the behavior has none and the project has a test setup.
   - For UI and runtime behavior, run the app and look at the change.

   A change you cannot prove goes in the PR's test plan as an open check.
   - Done when: every change in the diff has proof or an open check, and every check you ran passes.

   **Trace criteria.** Map each acceptance criterion to the test, file, or behavior that proves it. A fixture or artifact a ticket names must be the real one. Anything unmapped is fixed or reported as deferred. When the ticket file tracks status, tick the criteria and update its status.
   - Done when: no criterion is unmapped and the ticket reflects the result.

4. **Commit.** Commit completed slices with the `/commit` skill (required, do not commit outside it). Repeat until all intended changes are committed.
   - Done when: `git status` shows a clean tree for the intended work.

5. **Review.** Dispatch a subagent to run the `/review` skill on this branch. Give it the base from step 1, and the ticket or spec path, else the user's ask verbatim. When an earlier review exists, from this run or an earlier one, also give it that report and the findings declined so far, as findings the owner waived.

   Answer every finding in the report. Fix each one you agree with by the smallest change, proved and committed through steps 3 and 4. Decline the rest, each with a one-line reason and its evidence, such as a `path:line`, a test or command output. After a review that led to a fix, dispatch a follow-up review the same way, up to three reviews in all.
   - Done when: every finding is fixed or declined, and the last review led to no fix or was the third.

6. **PR.** Open or update the pull request with the `/to-pr` skill (required, do not create or edit PRs outside it), targeting the base from step 1. Give it a review report for a `## Review` heading in the body: the last review's opening lines, then the findings you declined, in the review's table with a column for your reason. With nothing declined, the report says "No open findings" in place of the table. Fixes made after the review go through steps 3 to 5 again, so the table in the body always matches the pushed commits.
   - Done when: `/to-pr` has returned the PR URL.
