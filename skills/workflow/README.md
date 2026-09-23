# Workflow

Deliver tickets, a spec, or substantive code or configuration changes through to a PR ready for review.

## Delivery

Use [implement](implement/SKILL.md) for the full delivery workflow:

```text
implement → commit → to-pr
```

It implements and verifies the change, then uses [commit](commit/SKILL.md) to create commits and [to-pr](to-pr/SKILL.md) to open or update the PR.

You can also use the skills independently:

- **commit** — Commit working-tree changes or prepare proposed batches without committing.
- **to-pr** — Open a PR from committed changes or refresh an existing PR description.

All three delivery skills support explicit invocation and automatic selection when relevant.

## Optional planning

Explicitly invoke [bootstrap-planning-skills](bootstrap-planning-skills/SKILL.md) in the target repository to install Matt Pocock's planning skills, run `/setup-matt-pocock-skills`, and document the pipeline in `AGENTS.md`:

```text
grill → spec → tickets → implement
```

Bootstrap is explicit-only. Planning is optional: you can start with `implement` when the requested change is already clear.
