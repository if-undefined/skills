---
name: commit
description: Commit or prepare commit batches.
---

# Commit

## Workflow

1. Inspect the current git state:
   - `git status`
   - `git diff` for unstaged changes
   - `git diff --staged` for staged changes
   - `git log --oneline -n 10` to match existing commit style
   If the working tree includes unexpected or unrelated changes, pause and confirm how to proceed.
2. Produce an ordered list of batches — each with its files and commit message — before staging. One concern per commit. Match completed todos, milestones, or coherent slices of work. If a subject line cannot carry the purpose, split the batch.
3. If the user only wants proposed batches, present the list, then stop.
4. Stage only the files for the current batch.
5. Commit with a message in the format below.
6. Repeat for additional batches if needed.
7. Stop after commit creation. Do not push unless the user explicitly asks.

## Commit message format

Use conventional commits: `<type>(<scope>): <subject>` in imperative mood.

Keep messages to a single line. Focus on the purpose of the change, not a file-by-file changelog.

**Example:**

```
feat(auth): implement JWT-based authentication
```

## Guardrails

- Do not use destructive git commands unless the user explicitly requests them.
- Do not co-author commits by the agent in the message.
