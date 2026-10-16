---
name: review
description: Review a branch or pull request against the project rules and its ticket or spec.
---

# Review

Read the change **cold**: as a reviewer who did not write it, trusting the diff and the files over any summary of them. Report what is worth changing before merge; the reader decides what to fix. A sound branch gets "No findings", and that is a complete review.

1. **Scope.** Given a pull request that isn't checked out, check it out with `gh pr checkout <number>`. Resolve the base: the base you were given, else the open PR's base, else the default branch. Fetch, and use the remote ref (`origin/<branch>`) for the last two. Establish the intent: the ticket or spec the branch implements, else the ask you were given or the PR description. Find any earlier report: the one you were given, else the `## Review` section of the open PR's body. Then choose the mode, which sets the change under review:
   - **Follow-up**: the earlier report names the commit it reviewed, and `git merge-base --is-ancestor <reviewed> HEAD` succeeds. The change is the branch's own commits since that review: `git log -p --no-merges <reviewed>..HEAD ^<base>`.
   - **Full review**: otherwise, or when asked for one. The change is the three-dot diff against the base.

   Add the paths in `git status`, untracked files included, and read each changed path in full.
   - Done when: the mode is chosen, every changed path has been read in full, and the intent's source is named (ticket path, spec path, the given ask, or the PR description).

2. **Requirements.** In a full review, map each acceptance criterion, or each part of the stated intent, to the code and the test that prove it. An unmapped criterion or part is a candidate finding. In a follow-up, mark each blocking finding in the earlier report as resolved (naming the commit), still open, or waived by the owner.
   - Done when: in a full review, every criterion or part is mapped or is a candidate; in a follow-up, every earlier blocking finding is marked.

3. **Defects.** Trace the changed code through its inputs, edge cases, failure paths and callers for defects: wrong behaviour, security holes and data loss. Apply the project rules in `AGENTS.md`, and in any rule files it points to, to the changed lines, and each installed unslop skill to the changed files in its stack. Each defect or broken rule is a candidate.
   - Done when: every changed function has been traced, and every rule applied to every changed line.

4. **Suggestions.** Full reviews only. Weigh the judgement calls on the changed code:
   - **Consistency**: the change follows the codebase's existing idioms: where each kind of code lives, how its recurring units (handlers, services, queries, components) are shaped, and how things are named. A new pattern where an existing one fits is a candidate.
   - **Simplest form**: each function is short, single-purpose and low in branching. Every piece of state, parameter, type, abstraction and file is one the behaviour needs. Code the change left unused is removed.
   - Done when: every changed path has been weighed against both calls.

5. **Substantiate.** Re-read the code behind each candidate. Keep the ones that pass one of these tests, and drop the rest:
   - **Blocking**: an unmet requirement, or a defect or broken rule the change introduced, on a changed line or in code the change breaks. Its evidence is the requirement or rule it breaks, or an input or state, reachable in the code as it stands, that triggers the defect.
   - **Suggestion**: a candidate from step 4 that names the existing code to match, with its path, or the code the behaviour doesn't need. Keep up to three, the ones that most improve the change.
   - Done when: every candidate has been re-read, and every kept finding passes its test.

6. **Report.** Open with the mode, the reviewed commit (`git rev-parse --short HEAD`), the base and the intent's source. A follow-up then lists each earlier blocking finding with its mark. Then one table, blocking findings first:

   | #   | Severity | Location | Issue | Evidence |
   | --- | -------- | -------- | ----- | -------- |

   Location is `path:line`, and Severity is Blocking or Suggestion. Earlier blocking findings that are still open stay in the table.

   With no findings, write "No findings" in place of the table.
   - Done when: the report opens with its mode and reviewed commit, and every kept or still-open finding is in the table, or "No findings" is stated.
