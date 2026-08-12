# Workflow

The intended use of these skills is to allow an agent to deterministically implement a well-defined specification or ticket, up to the point of code-review. Implement from a spec or tickets, verify, commit, and create a PR for review.

This workflow begins with a well-defined specification or ticket. Use **bootstrap-planning-skills** to install Matt Pocock's planning pipeline (grill → spec → tickets) in a target repo on demand.

## User Invoked

Run explicitly by the user.

* **bootstrap-planning-skills** — Install Matt Pocock's planning skills in a target repo, run `/setup-matt-pocock-skills`, and document the grill → spec → tickets → implement pipeline.
* **implement** — Branch, build, verify, commit, and create a PR for your review.

## Model Invoked

Available to both the workflow and the user when needed.

* **commit** — Commit or prepare commit batches.
* **to-pr** — Create or update a GitHub PR for review.
