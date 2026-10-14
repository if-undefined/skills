---
name: review
description: Review a branch or pull request against the project rules and its ticket or spec.
---

# Review

Read the change **cold**: as a reviewer who did not write it, trusting the diff and the files over any summary of them. Report findings; the reader decides what to fix.

1. **Scope.** Given a pull request that isn't checked out, check it out with `gh pr checkout <number>`. Resolve the base: the base you were given, else the open PR's base, else the default branch. Fetch, and use the remote ref (`origin/<branch>`) for the last two. Collect the changed paths from the three-dot diff against it and from `git status`, untracked files included, then read each in full. Establish the intent: the ticket or spec the branch implements, else the ask you were given or the PR description.
   - Done when: every changed path has been read in full, and the intent's source is named (ticket path, spec path, the given ask, or the PR description).

2. **Requirements.** Map each acceptance criterion, or each part of the stated intent, to the code and the test that prove it.
   - Done when: every criterion or part is mapped, or reported as a High finding.

3. **Rules.** Apply every file in `.agents/rules/` to every changed path, and `/react-effects` to changed components. Beyond each rule's wording, weigh the judgement calls:
   - **Consistency**: the change does what neighbouring code already does: where types, labels, helpers and components live, and how pages, forms, queries and actions are shaped. A new pattern where an existing one fits is a finding.
   - **Simplest form**: each function is short, single-purpose and low in branching. Every piece of state, prop, parameter, abstraction and file is one the behaviour needs. Code the change left unused is removed.
   - Done when: every rule file has been applied to every changed path.

4. **Report.** One table, most severe first:

   | #   | Severity | Location | Issue | Evidence |
   | --- | -------- | -------- | ----- | -------- |

   Location is `path:line`. Evidence is the rule, requirement, existing code or principle the finding rests on. Severity:
   - **High**: wrong behaviour, data loss, security, or an unmet requirement.
   - **Medium**: names something concrete to change: a broken rule, an existing pattern to match (with its path), or code the behaviour doesn't need.
   - **Low**: a preference with nothing concrete to point to.
   - **Info**: a note with nothing to change.

   With no findings, write "No findings" in place of the table.
   - Done when: every finding has a location and evidence, or "No findings" is stated.
