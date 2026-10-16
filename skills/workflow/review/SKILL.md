---
name: review
description: Review a branch or pull request against the project rules and its ticket or spec.
---

# Review

Read the change **cold**: as a reviewer who did not write it, trusting the diff and the files over any summary of them. Report what is worth changing before merge; the reader decides what to fix. A sound branch gets "No findings", and that is a complete review.

1. **Scope.** Given a pull request that isn't checked out, check it out with `gh pr checkout <number>`. Resolve the base: the base you were given, else the open PR's base, else the default branch. Fetch, and use the remote ref (`origin/<branch>`) for the last two. Collect the changed paths from the three-dot diff against it and from `git status`, untracked files included, then read each in full. Establish the intent: the ticket or spec the branch implements, else the ask you were given or the PR description.
   - Done when: every changed path has been read in full, and the intent's source is named (ticket path, spec path, the given ask, or the PR description).

2. **Requirements.** Map each acceptance criterion, or each part of the stated intent, to the code and the test that prove it. An unmapped criterion or part is a candidate finding.
   - Done when: every criterion or part is mapped or is a candidate.

3. **Defects.** Trace the changed code through its inputs, edge cases, failure paths and callers for wrong behaviour, security holes and data loss. Apply the project instructions in `AGENTS.md`, and any rule files it points to, to every line the change adds or modifies, and each installed unslop skill to the changed files in its stack. Each problem you find is a candidate.
   - Done when: every changed function has been traced, and every instruction applied to every changed line.

4. **Suggestions.** Weigh the judgement calls on the code the change adds or modifies:
   - **Consistency**: the change follows the codebase's existing idioms: where each kind of code lives, how its recurring units (handlers, services, queries, components) are shaped, and how things are named. A new pattern where an existing one fits is a candidate.
   - **Simplest form**: each function is short, single-purpose and low in branching. Every piece of state, parameter, type, abstraction and file is one the behaviour needs. Code the change left unused is removed.
   - Done when: both calls have been weighed across the change.

5. **Verify.** Re-read the code behind each candidate. Keep the ones that pass one of these tests, and drop the rest:
   - **Blocking**: an unmet requirement, or a problem the change introduced on a line it adds or modifies or in code it breaks. Its evidence is the requirement or rule text it breaks, or an input or state, reachable in the code as it stands, that produces wrong behaviour, a security hole or data loss.
   - **Suggestion**: a candidate from step 4 that names the existing code to match, with its path, or the code the behaviour doesn't need. Keep up to three, the ones that most improve the change.
   - Done when: every kept finding passes its test, with at most three suggestions.

6. **Report.** One table, blocking findings first:

   | #   | Severity | Location | Issue | Evidence |
   | --- | -------- | -------- | ----- | -------- |

   Location is `path:line`, and Severity is Blocking or Suggestion. Evidence is the consequence, requirement, rule or existing code from step 5.

   With no findings, write "No findings" in place of the table.
   - Done when: every kept finding is in the table, or "No findings" is stated.
