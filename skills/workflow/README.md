# Workflow

Deterministic delivery up to code review: branch, build, verify, commit, and open a PR. Agents should defer to **implement** when making substantive code or configuration changes in a repository.

Optional planning upfront: use **bootstrap-planning-skills** to install Matt Pocock's planning pipeline (grill → spec → tickets) in a target repo on demand.

## User Invoked

Run explicitly by the user.

* **bootstrap-planning-skills** — Install Matt Pocock's planning skills in a target repo, run `/setup-matt-pocock-skills`, and document the grill → spec → tickets → implement pipeline.

## Model Invoked

Available to both the workflow and the user when needed.

* **implement** — Branch, build, verify, commit, and create a PR for review.
* **commit** — Commit or prepare commit batches.
* **to-pr** — Create or update a GitHub PR for review.
