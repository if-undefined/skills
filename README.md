## Skills

A repository of my daily skills.

### Available skills

* [**workflow**](skills/workflow/) — Implement from a spec or tickets, verify, and commit.
  * **implement** (user-invoked) — Branch, build, verify, then commit via the commit skill.
  * **commit** (model-invoked) — Commit or prepare commit batches.

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