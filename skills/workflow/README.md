# Workflow

The intended use of these skills is to allow an agent to deterministically implement a well-defined specification or ticket, up to the point of code-review. Implement from a spec or tickets, verify, commit, and create a PR for review.

This workflow begins with a well-defined specification or ticket. Specification generation sits outside this folder.

## User Invoked

Run explicitly by the user.

* **implement** — Branch, build, verify, commit, and create a PR for your review.

## Model Invoked

Available to both the workflow and the user when needed.

* **commit** — Commit or prepare commit batches.
* **to-pr** — Create or update a GitHub PR for review.
