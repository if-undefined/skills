# Workflow

Skills that carry software changes through the repository workflow: implementing an already-produced specification, organizing and committing changes, and creating pull requests.

Specification generation belongs elsewhere. Workflow skills consume specifications and manage implementation and delivery.

## User-invoked

Reachable only when you type them (Claude Code: `disable-model-invocation: true`; Codex: `policy.allow_implicit_invocation: false` in `agents/openai.yaml`).

* **implement** — Implement work from a spec or tickets: branch, build, verify, then commit via the commit skill.

## Model-invoked

Model- or user-reachable (rich trigger phrasing so the model can reach for them).

* **commit** — Commit or prepare commit batches.
