---
name: bootstrap-planning-skills
description: Bootstrap a target repo with Matt Pocock's planning skills (grill → spec → tickets).
disable-model-invocation: true
---

# Bootstrap planning skills

Install Matt Pocock's engineering planning skills in the **target repo** (where this skill is invoked), run `/setup-matt-pocock-skills` for per-repo configuration, and document the planning pipeline in `AGENTS.md`. Delivery stays in existing workflow skills (`/implement` → `/commit` → `/to-pr`).

All installs and writes happen in the target repo — not in `if-undefined/skills`.

## Workflow

1. **Preflight** — Confirm the current working directory is a git repo (`git rev-parse --is-inside-work-tree`). Read `git remote -v`. Check for `.agents/skills/` and `docs/agents/`. If planning skills are already installed (e.g. `grill-with-docs`, `to-spec`, `to-tickets`, or `setup-matt-pocock-skills` under `.agents/skills/`), report what's present and ask whether to re-run setup or stop.
   - Done when: starting state is recorded and the user has confirmed to proceed (or chosen to stop).

2. **Install** — In the target repo, run:

   ```bash
   pnpm dlx skills@latest add mattpocock/skills \
     --skill grill-with-docs \
     --skill grilling \
     --skill domain-modeling \
     --skill to-spec \
     --skill to-tickets \
     --skill setup-matt-pocock-skills \
     -y
   ```

   Do not vendor or copy skill bodies into the target repo — the CLI installs them at runtime.
   - Done when: six skill folders exist under `.agents/skills/` and `skills-lock.json` is updated.

3. **Configure (delegate)** — Run `/setup-matt-pocock-skills` in full. That skill owns all repo configuration:
   - `docs/agents/issue-tracker.md`
   - `docs/agents/domain.md`
   - `docs/agents/triage-labels.md` (only when `triage` is installed)
   - The `## Agent skills` block in `AGENTS.md` or `CLAUDE.md` (issue tracker, domain docs, triage labels)

   Do **not** manually create, copy, or write any of those files or sections in this skill. Do not bundle reference templates for them. If setup needs user input, follow its interactive flow — do not shortcut with hardcoded defaults that bypass `/setup-matt-pocock-skills`.
   - Done when: `/setup-matt-pocock-skills` has completed per its own completion criteria.

4. **Skill workflows** — After `/setup-matt-pocock-skills` finishes, add or update **only** a `### Skill workflows` subsection under the existing `## Agent skills` block. Use this content:

   ```markdown
   ### Skill workflows

   - **Greenfield feature** — `/grill-with-docs` → `/to-spec` → `/to-tickets` → `/implement`
   - **Quick stress-test** — `/grilling` (switch to `/grill-with-docs` to persist domain docs)
   - **Conversation already settled** — `/to-spec` directly, then `/to-tickets` if needed
   - **Codebase audit** — `/improve` (plans in `plans/`; optionally feed `/to-tickets` for GitHub-tracked execution)
   ```

   Merge in-place if `### Skill workflows` already exists. Do not duplicate or overwrite `/setup-matt-pocock-skills`' subsections.
   - Done when: the workflows section is present and references `/implement` (not inline implementation steps).

5. **Report** — Summarize what was bootstrapped, that config was produced by `/setup-matt-pocock-skills`, the planning pipeline (`grill → spec → tickets → implement`), and any manual follow-ups (optional `triage` skill later).
   - Done when: the user knows how to start the pipeline.

## Guardrails

- **Target repo only** — all installs and writes happen in the repo where this skill is invoked, not in `if-undefined/skills`.
- **No implementation** — do not branch, code, lint, or open PRs in the target repo unless the user explicitly asks beyond this skill's scope.
- **Defer config to setup-matt-pocock-skills** — never manually write `docs/agents/*` or setup's `## Agent skills` subsections. The only `AGENTS.md` / `CLAUDE.md` addition this skill makes is `### Skill workflows`.
- **Compose, don't duplicate** — install → `/setup-matt-pocock-skills` → add skill workflows.
- **Do not install `triage` or `wayfinder`** unless the user explicitly requests them.
