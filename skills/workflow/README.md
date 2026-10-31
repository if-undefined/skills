# Workflow

Deliver a change through to a draft PR when a request says "implement".

## Delivery

Use [implement](implement/SKILL.md) for the full delivery workflow. It runs when a request says "implement", so a request without the word gets a direct edit instead:

```text
implement → commit → review → to-pr
```

It implements and proves the change, then uses [commit](commit/SKILL.md) to create commits and [review](review/SKILL.md) to review the branch. It fixes the findings it agrees with and reviews again, up to three reviews, then uses [to-pr](to-pr/SKILL.md) to open or update the PR with the findings it declined.

You can also use the skills independently:

- **commit** — Commit working-tree changes or prepare proposed batches without committing.
- **review** — Review a branch or pull request against the project rules and its ticket or spec. On a PR it has reviewed before, it checks only the commits since; ask for a full review to start over.
- **to-pr** — Open a PR from committed changes or refresh an existing PR description.

All three delivery skills support explicit invocation and automatic selection when relevant.

## Optional planning

Explicitly invoke [bootstrap-planning-skills](bootstrap-planning-skills/SKILL.md) in the target repository to install Matt Pocock's planning skills, run `/setup-matt-pocock-skills`, and document the pipeline in `AGENTS.md`:

```text
grill → spec → tickets → implement
```

Bootstrap is explicit-only. Planning is optional: you can start with `implement` when the requested change is already clear.
