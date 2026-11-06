---
name: commit
description: Use for every commit, of any size.
---

# Commit

## Workflow

1. Inspect the current git state:
   - `git status`
   - `git diff` for unstaged changes
   - `git diff --staged` for staged changes
   - `git log --oneline -n 10` to match the wording of recent subjects
2. Batch the changes that belong to the current task, or, with no task, every change that belongs in the project's history. Produce an ordered list of batches — each with its files and commit message — before staging. One concern per commit. Match completed todos, milestones, or coherent slices of work. If a subject line cannot carry the purpose, split the batch.
3. Stage only the files for the current batch.
4. Commit with a message in the format below. If a pre-commit hook fails, address the violations it reports and retry.
5. Repeat for additional batches if needed.
6. Push only when the user explicitly asks.

## Commit message format

Use conventional commits: `<type>: <subject>` in imperative mood.

Keep messages to a single line. Focus on the purpose of the change, not a file-by-file changelog.

**Example:**

```
feat: implement JWT-based authentication
```

## Guardrails

- Do not use destructive git commands unless the user explicitly requests them.
- Do not co-author commits by the agent in the message.
