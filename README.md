# Skills

A repository of my daily skills. These are a work-in-progress.

Disclaimer; this repository has been inspired by [Matt Pocock's](https://github.com/mattpocock/skills) skills.

## Available skills

I've split these skills into use-cases and in most cases, will depend on another skill in that same use-case to function. 

### Workflow

The intended use of these skills is to allow an agent to deterministically implement a well-defined specification or ticket, up to the point of code-review. Implement from a spec or tickets, verify, and commit.

#### Prerequisites

This workflow depends on a collection of well-defined specifications or tickets for an agent to begin implementing.

I would recommend using [grill-with-docs](https://github.com/mattpocock/skills/blob/main/skills/engineering/grill-with-docs/SKILL.md) until you have a shared understanding of your application and the feature or task you wish to implement.

To quickly get started, the following will install the required skill and its dependencies:

```
pnpm dlx skills@latest add mattpocock/skills \ 
  --skill grill-with-docs \
  --skill grilling \
  --skill domain-modeling \
  --skill to-spec \
  --skill to-tickets \
  --skill setup-matt-pocock-skills \
  -y
```

First, run `setup-matt-pocock-skills` and then `grill-with-docs`.

#### User Invoked

  * [**implement**](skills/implement) — Branch, build, verify, commit and create a PR for your review.

#### Model Invoked

  * [**commit**](skills/commit) — Commit or prepare commit batches.
  * [**to-pr**](skills/to-pr) - Create or update an PR in Github for review.


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