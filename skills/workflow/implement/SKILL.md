---
name: implement
description: >-
  Implement tickets or a spec through to a pull request. Also use for
  substantive code or configuration changes without one.
---

# Implement

1. **Branch** — If the current branch is `master` or `main`, create and check out a new branch named from the ticket id plus a short kebab slug when a ticket exists (e.g. `42-add-login`); otherwise a kebab slug from the change intent.
   - Done when: HEAD is not on `master`/`main`, and the branch name matches that pattern.

2. **Build** — Implement against the tickets or spec until their acceptance criteria are met. Prefer the narrowest change that satisfies them. When neither is present, implement the user's ask the same way.
   - Done when: every acceptance criterion (or stated ask) is satisfied (or explicitly deferred by the user).

3. **Verify** — Discover the project's checks from the environment (package scripts, Makefile, CI config — e.g. tests, lints, typecheck, build) and run them after each substantive slice, and once more when the build step is complete.
   - Done when: every check the project defines has been run and passes.

4. **Commit** — Commit completed slices with the `/commit` skill (required — do not commit outside it). Repeat until all intended changes are committed.
   - Done when: `git status` shows a clean tree for the intended work.

5. **PR** — Open or update the pull request with the `/to-pr` skill (required — do not create or edit PRs outside it).
   - Done when: `/to-pr` has returned the PR URL.
