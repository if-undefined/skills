---
name: implement
description: "Implement work from a spec or tickets."
disable-model-invocation: true
---

# Implement

1. **Branch** — If the current branch is `master` or `main`, create and check out a new branch named from the ticket id plus a short kebab slug (e.g. `42-add-login`), or a kebab slug from the spec title when there is no ticket.
   - Done when: HEAD is not on `master`/`main`, and the branch name matches that pattern.

2. **Build** — Implement against the user's spec or tickets until their acceptance criteria are met. Prefer the narrowest change that satisfies them.
   - Done when: every acceptance criterion in the spec/tickets is satisfied (or explicitly deferred by the user).

3. **Verify** — Discover the project's checks from the environment (package scripts, Makefile, CI config — e.g. tests, lints, typecheck, build) and run them after each substantive slice, and once more when the build step is complete.
   - Done when: every check the project defines has been run and passes.

4. **Commit** — Commit completed slices with the `/commit` skill (required — do not commit outside it). Repeat until all intended changes are committed.
   - Done when: `git status` shows a clean tree for the intended work.
