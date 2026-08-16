# Skills

A repository of my daily skills. These are a work-in-progress.

Disclaimer; this repository has been inspired by [Matt Pocock's](https://github.com/mattpocock/skills) skills.

## Available skills

I've split these skills into use-cases and in most cases, will depend on another skill in that same use-case to function. 

### Workflow

Deterministic delivery up to code review: branch, build, verify, commit, and open a PR. Agents should defer to **implement** when making substantive code or configuration changes in a repository.

#### Prerequisites

Optional planning upfront: run [**bootstrap-planning-skills**](skills/workflow/bootstrap-planning-skills) in your target repo to install Matt Pocock's planning skills (grill → spec → tickets), configure the repo via `/setup-matt-pocock-skills`, and document the pipeline in `AGENTS.md`. Delivery stays in the workflow skills below.

#### User Invoked

  * [**bootstrap-planning-skills**](skills/workflow/bootstrap-planning-skills) — Bootstrap a target repo with Matt Pocock's planning pipeline.

#### Model Invoked

  * [**implement**](skills/workflow/implement) — Branch, build, verify, commit, and create a PR for review.
  * [**commit**](skills/workflow/commit) — Commit or prepare commit batches.
  * [**to-pr**](skills/workflow/to-pr) - Create or update an PR in Github for review.


## Installation

Requires [Node.js](https://nodejs.org/) and the [Skills CLI](https://github.com/vercel-labs/skills).

```bash
npx skills add if-undefined/skills
```

The CLI will prompt you to choose which skills to install and which agents to install them on.

### Updating

```bash
npx skills update
```