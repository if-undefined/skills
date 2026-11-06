---
name: to-pr
description: Pull requests. Open one or refresh an existing PR description.
---

# Create or update a pull request

## Workflow

1. **Resolve scope.** Determine the current branch, its existing PR (if any), and the actual base: use the existing PR base when updating; otherwise use the remote default branch unless the user named one. Done when the comparison range is fixed.
2. **Commit the work.** The PR represents committed changes only. Commit the dirty changes that belong to the branch's work, judged from its commits and the changes themselves, creating a branch first when HEAD is on the base. Leave every other path out of the commits, without asking about it. Done when every dirty path is committed or left out as unrelated, and the comparison range has at least one committed change.
3. **Read the whole change.** Inspect every commit and the complete three-dot diff against the resolved base; read linked issue/spec material when it explains intent. Done when every commit and every changed path in the three-dot diff has been inspected.
4. **Draft.** Fill the title and body per *Title and body* below, using branch intent and behavior rather than a file inventory. Done when every changed area is represented or deliberately omitted as implementation detail, every retained section is specific and evidence-backed, and every row of an existing `## Review` table has been checked against `HEAD`.
5. **Publish.** Normal-push committed `HEAD` when the remote needs it (history rewrite requires separate explicit approval), then create a draft PR with `gh pr create --draft` or update with `gh pr edit`. The author marks the PR ready for review, which starts CI that skips drafts. Leave an existing PR's draft state as it is. Pass multiline body content via a HEREDOC. Done when GitHub returns the PR and its body matches the text from step 4.
6. **Report.** Return the linked PR URL, say whether it is a draft, and distinguish completed automated checks from outstanding manual checks. Done when the response contains the PR URL and its draft state, and distinguishes completed automated checks from outstanding manual checks.

Authentication failure is a blocker to report after the environment's normal credential/permission retry; never ask the user to paste a token.

## Title and body

For a new PR, use the repository's conventional-commit title shape and name the branch's purpose. Preserve an existing title during a description-only update.

The body contains change information only, without agent attribution. Drop "What's in this branch" when it would repeat Summary. Mark a test-plan checkbox complete only when its passing result is available to the current agent; never infer execution from files or commit messages.

A `## Review` table describes `HEAD`. Replace the section with a newer review report when you were given one. Otherwise carry it over, removing each row that commits since the review resolved, naming the resolving commit beneath the table's intro line, and renumbering the remaining rows. The next review follows up from the section.

```markdown
## Summary
- <1-3 bullets explaining why the change exists and its user/domain outcome>

## What's in this branch
### <behavioral grouping>
- <notable behavior or architectural decision>

## Test plan
- [x] <check known to have passed in this session/context>
- [ ] <manual or automated check still outstanding>
```
