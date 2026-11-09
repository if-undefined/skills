---
name: review
description: Review a branch or pull request against the project rules and its ticket or spec.
---

# Review

When a user invokes this skill directly, dispatch a fresh subagent to run it, giving it their request verbatim and telling it that it was dispatched, then relay its report unchanged. A dispatched reviewer starts at Scope.

Read the change **cold**: as a reviewer who did not write it, trusting the diff and the files over any summary of them. Report what is worth changing before merge; the reader decides what to fix. A sound branch gets "No findings", and that is a complete review.

## Steps

1. **Scope**: resolve the base and intent, choose the mode, and read every changed path.
2. **Requirements**: map the intent to the code, or mark the earlier report's blocking findings.
3. **Defects**: trace the changed code and apply the project rules.
4. **Suggestions**: weigh the judgement calls, in full reviews only.
5. **Substantiate**: re-read each candidate and keep the ones that pass their test.
6. **Report**: open with the review's details, then table the findings.

## Scope

If you were given a pull request, check it out. Then establish:

- **Base**: the base you were given, else the latest remote copy of the open PR's base, else of the default branch.
- **Intent**: the ticket or spec the branch implements, else the ask you were given or the PR description.
- **Mode**: **Follow-up** when your request includes an earlier report and the commit it reviewed is still in the branch's history. Otherwise **Full review**.
- **Change**: in a full review, everything the branch changes since it left the base. In a follow-up, only the commits the branch itself added since the reviewed commit, excluding merges and anything from the base. In both, add the uncommitted work, including untracked files, in paths the change touches or the intent covers. When a full review's change is empty, add all uncommitted work.

Read each changed path in full. With no changed paths, stop and report "Nothing to review", naming the base and `HEAD`.

Done when: the mode is chosen, every changed path has been read in full, and the intent's source is named (ticket path, spec path, the given ask, or the PR description).

## Requirements

In a full review, map each acceptance criterion, or each part of the stated intent, to the code and the test that prove it. An unmapped criterion or part is a candidate finding. In a follow-up, mark each blocking finding in the earlier report as resolved by a named commit, as still open, or as declined when the earlier report or the request gives a reason for declining it.

Done when: in a full review, every criterion or part is mapped or is a candidate; in a follow-up, every earlier blocking finding is marked.

## Defects

Trace the changed code through its inputs, edge cases, failure paths and callers for defects: wrong behaviour, security holes and data loss. Apply the project rules in `AGENTS.md`, and in any rule files it points to, to the changed lines, and each installed unslop skill to the changed files in its stack. Each defect or broken rule is a candidate.

Done when: every changed function has been traced, and every rule applied to every changed line.

## Suggestions

Full reviews only. Weigh the judgement calls on the changed code:

- **Consistency**: the change follows the codebase's existing idioms: where each kind of code lives, how its recurring units (handlers, services, queries, components) are shaped, and how things are named. A new pattern where an existing one fits is a candidate.
- **Simplest form**: each function is short, single-purpose and low in branching. Every piece of state, parameter, type, abstraction and file is one the behaviour needs. Code the change left unused is removed.
- **Asked for**: when a ticket, spec or ask describes the change, each behaviour the change adds is one it asks for. Added behaviour it doesn't mention is a candidate.

Done when: every changed path has been weighed against all three calls.

## Substantiate

Re-read the code behind each candidate. Keep the ones that pass one of these tests, and drop the rest:

- **Blocking**: an unmet requirement, or a defect or broken rule the change introduced, on a changed line or in code the change breaks. Its evidence is the requirement or rule it breaks, or an input or state, reachable in the code as it stands, that triggers the defect.
- **Suggestion**: a candidate from Suggestions that names the existing code to match, with its path, the code the behaviour doesn't need, or the behaviour the intent doesn't ask for. Keep up to three, the ones that most improve the change.

Done when: every candidate has been re-read, and every kept finding passes its test.

## Report

Open with the mode, the reviewed commit (`git rev-parse --short HEAD`), the base and the intent's source. A follow-up then lists each earlier blocking finding with its mark. Then one table, blocking findings first:

| #   | Severity | Location | Issue | Evidence |
| --- | -------- | -------- | ----- | -------- |

Location is `path:line`, and Severity is Blocking or Suggestion. Earlier blocking findings that are still open stay in the table.

With no findings, write "No findings" in place of the table.

Done when: the report opens with its mode and reviewed commit, and every kept or still-open finding is in the table, or "No findings" is stated.
