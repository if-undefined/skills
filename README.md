# Skills

My everyday agent skills. A work in progress, inspired by [Matt Pocock's skills](https://github.com/mattpocock/skills).

## Available skills

| Skill | Purpose |
| --- | --- |
| [implement](skills/workflow/implement/SKILL.md) | Deliver tickets, a spec, or substantive code or configuration changes through to a PR. |
| [commit](skills/workflow/commit/SKILL.md) | Commit changes or prepare commit batches. |
| [to-pr](skills/workflow/to-pr/SKILL.md) | Open a GitHub PR or refresh an existing PR description. |
| [bootstrap-planning-skills](skills/workflow/bootstrap-planning-skills/SKILL.md) | Set up Matt Pocock's planning pipeline in a target repository. |

See the [workflow guide](skills/workflow/README.md) for invocation and optional planning setup.

## Installation

Requires [Node.js](https://nodejs.org/). Install with the [Skills CLI](https://github.com/vercel-labs/skills):

```bash
npx skills add if-undefined/skills
```

Choose which skills to install and which agents to install them for when prompted.

### Updating

```bash
npx skills update
```
