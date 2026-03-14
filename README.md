# Agent Skills

Skills for agents that support the official [`skills`](https://skills.sh/) CLI.

## Included skills

- `docs-architecture`: Maintain system and domain architecture docs such as `docs/ARCHITECTURE.md`, `web-architecture.md`, or `api-architecture.md`.
- `docs-components-design`: Maintain technical design docs for services, components, workers, modules, and APIs.
- `docs-feature-design`: Maintain feature docs that explain user-visible behavior, goals, flows, and business rules without implementation detail.

## Installation

Install every skill:

```bash
npx --yes skills add onatm/agent-skills
```

Install a single skill:

```bash
npx --yes skills add onatm/agent-skills --skill docs-feature-design
```

## Verify compatibility

This repository is structured as a multi-skill source that the official CLI can discover directly from the repository root. To verify that locally:

```bash
npx --yes skills add . --list
```
