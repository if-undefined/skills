---
name: to-pr
description: >-
  Pull requests: creates one from the committed branch diff or updates an
  existing PR description. Use when opening a PR or refreshing its description.
---

# PR create/update

## Workflow

1. **Resolve scope.** Determine the current branch, its existing PR (if any), and the actual base: use the existing PR base when updating; otherwise use the remote default branch unless the user named one. Done when the comparison range is fixed and has at least one committed change.
2. **Account for the working tree.** The PR represents committed changes only. If dirty changes appear intended for this PR, pause for `/commit`; otherwise leave them untouched and continue. Done when every dirty path is classified as included-later or unrelated.
3. **Read the whole change.** Inspect every commit and the complete three-dot diff against the resolved base; read linked issue/spec material when it explains intent. Done when every commit and every changed path in the three-dot diff has been inspected.
4. **Draft.** Fill the title and body per *Title and body* below, using branch intent and behavior rather than a file inventory. Done when every changed area is represented or deliberately omitted as implementation detail, and every retained section is specific and evidence-backed.
5. **Publish.** Normal-push committed `HEAD` when the remote needs it (history rewrite requires separate explicit approval), then create with `gh pr create` or update with `gh pr edit`. Pass multiline body content via a HEREDOC. Done when GitHub returns the PR and its body matches the draft.
6. **Report.** Return the linked PR URL and distinguish completed automated checks from outstanding manual checks. Done when the response contains the PR URL and distinguishes completed automated checks from outstanding manual checks.

Authentication failure is a blocker to report after the environment's normal credential/permission retry; never ask the user to paste a token.

## Title and body

For a new PR, use the repository's conventional-commit title shape and name the branch's purpose. Preserve an existing title during a description-only update.

The body contains change information only, without agent attribution. Drop "What's in this branch" when it would repeat Summary. Mark a test-plan checkbox complete only when its passing result is available to the current agent; never infer execution from files or commit messages.

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
