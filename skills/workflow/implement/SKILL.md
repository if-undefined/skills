---
name: implement
description: Implement tickets or a spec through to a pull request. Also use for substantive code or configuration changes without either.
---

# Implement

1. **Branch.** When HEAD is already this work's branch, stay on it; its base is the open PR's base, else the base chosen below. Otherwise choose a base and branch from it:
   - Base: the remote default branch (`origin/<default>`) after a fetch, unless this work builds on commits that exist only on another unmerged branch (a **Blocked by** ticket's branch, or the branch checked out now). Then base on that branch.
   - Create: `git switch --no-track -c <name> <base>`; `--no-track` keeps a remote base from becoming the push target. Name it from the ticket id plus a short kebab slug when a ticket exists (e.g. `42-add-login`); otherwise a kebab slug from the change intent. Earlier work arrives only through the base.
   - Done when: HEAD is on this work's branch, its name matches that pattern, and `git merge-base --is-ancestor <base> HEAD` succeeds (a read-only check that HEAD contains every commit on the base).

2. **Build.** Implement against the tickets or spec until their acceptance criteria are met. Prefer the narrowest change that satisfies them. When neither is present, implement the user's ask the same way.
   - Done when: every acceptance criterion (or stated ask) is satisfied (or explicitly deferred by the user).

3. **Verify.** Discover the project's checks from the environment (package scripts, Makefile, CI config, such as tests, lints, typecheck, build) and run them after each substantive slice, and once more when the build step is complete.
   - Done when: every check the project defines has been run and passes.

   **Trace criteria.** Map each acceptance criterion to the test, file, or behavior that proves it. A fixture or artifact a ticket names must be the real one. Anything unmapped is fixed or reported as deferred. When the ticket file tracks status, tick the criteria and update its status.
   - Done when: no criterion is unmapped and the ticket reflects the result.

4. **Commit.** Commit completed slices with the `/commit` skill (required, do not commit outside it). Repeat until all intended changes are committed.
   - Done when: `git status` shows a clean tree for the intended work.

5. **Review.** Dispatch a subagent to run the `/review` skill on this branch. Give it the base from step 1, and the ticket or spec path, else the user's ask verbatim. Carry its report unchanged into your final report; the owner decides what to fix.
   - Done when: the review has returned its report.

6. **PR.** Open or update the pull request with the `/to-pr` skill (required, do not create or edit PRs outside it), targeting the base from step 1, with the review report under a `## Review` heading in the body.
   - Done when: `/to-pr` has returned the PR URL.
