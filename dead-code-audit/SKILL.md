---
name: dead-code-audit
description: Audit repositories for dead code, unreachable control flow, unused imports, and unused package dependencies, then triage cleanup candidates and produce a structured report. Use when asked to scan an entire codebase for dead code, technical-debt cleanup, unused exports, unreachable branches, phantom dependencies, or safe-to-delete files.
---

# Dead Code Audit

Audit a repository for dead code and cleanup candidates. Prefer project-native analyzers plus repository search, then verify each candidate before labeling it dead.

## Audit Flow

1. Map the repo.
- Identify languages, package managers, build targets, test entrypoints, code generation, and whether the repo is an application, internal service, or public library.
- Inspect manifest and inclusion boundaries first: `package.json`, `tsconfig*`, `pyproject.toml`, `go.mod`, `Cargo.toml`, Gradle/Maven files, workspace configs, bundler configs, and generated-code rules.
- Read [references/tool-selection.md](references/tool-selection.md) only for the relevant ecosystem.

2. Discover candidates.
- `UNREACHABLE_DECL`: functions, methods, variables, constants, types, classes, enums, interfaces, exports, or whole files with no live usage.
- `DEAD_FLOW`: constant conditions, unreachable branches, code after unconditional `return`/`throw`/`exit`, and feature flags fixed to one state.
- `PHANTOM_DEP`: unused imports within a file and manifest dependencies with no source usage.
- Record concrete evidence for every candidate: definition site, search or tool output, build exclusion status, and why it appears dead.

3. Verify before calling anything dead.
- Rule out dynamic dispatch, reflection, runtime type lookup, dependency injection containers, decorators, registries, serialization targets, ORM models, protobuf or schema bindings, macros, code generation, template expansion, test fixtures, and framework lifecycle hooks.
- Treat exported symbols in library packages as externally consumable unless the repo proves otherwise.
- Check config files, env-driven registries, route tables, CLI command maps, plugin manifests, and feature-flag registries for name-based references.
- If evidence is mostly negative evidence such as "no refs found," lower confidence and explain why.

4. Assign risk and action.
- `HIGH`: safe to delete immediately; no external callers, no framework magic, no config-driven references.
- `MEDIUM`: likely dead but indirect usage remains plausible; verify before deleting.
- `LOW`: probably used through reflection, configuration, framework hooks, generated code, or public API surface.
- `DELETE`: remove unused code with high confidence.
- `RENAME_TO_UNDERSCORE`: keep an intentionally unused local, parameter, or callback slot while silencing warnings.
- `MOVE_TO_ARCHIVE`: preserve code or files that appear obsolete but may still be needed for reference or rollback.
- `MANUAL_VERIFY`: require human confirmation before touching it.
- `SUPPRESS_WITH_COMMENT`: keep a symbol intentionally and document why analyzers should ignore it.

5. Build the report.
- Produce the three required sections in order.
- Sort findings by risk (`HIGH`, `MEDIUM`, `LOW`), then by confidence, then by file path.
- If nothing credible is dead, output an empty findings table, zeroed summary metrics, and a brief note describing what you checked and what limited certainty.

## Output Contract

### 1. Findings Table

Use this exact header:

| # | File | Line(s) | Symbol | Category | Risk | Confidence | Action |
|---|------|---------|--------|----------|------|------------|--------|

- Use repository-relative file paths.
- Use precise line numbers when possible.
- Write `Confidence` as `0.00-1.00`.
- Use only `UNREACHABLE_DECL`, `DEAD_FLOW`, or `PHANTOM_DEP` for `Category`.
- Use only `DELETE`, `RENAME_TO_UNDERSCORE`, `MOVE_TO_ARCHIVE`, `MANUAL_VERIFY`, or `SUPPRESS_WITH_COMMENT` for `Action`.
- Keep one finding per row.

### 2. Cleanup Roadmap

Create three sequential batches:
- Batch 1: `HIGH`
- Batch 2: `MEDIUM`
- Batch 3: `LOW`

For each batch, include:
- Estimated LOC removed
- Potential bundle or binary size impact
- Suggested refactoring order

Start with leaf files, unused imports, and clearly private symbols before shared modules or exported APIs.

### 3. Executive Summary

Use this exact header:

| Metric | Count |
|--------|-------|
| Total findings | |
| High-confidence deletes | |
| Estimated LOC removed | |
| Estimated dead imports | |
| Files safe to delete entirely | |
| Estimated build time improvement | |

- Keep estimates conservative.
- Use `unknown` when the repo does not provide enough evidence for a number.
- End with one paragraph assessing overall codebase health and the top three actions to take first.

## Working Rules

- Prefer compiler warnings, existing analyzers, and repo-native commands over intuition.
- Distinguish source, generated, vendored, test, and fixture code before counting findings.
- Evaluate monorepos package by package before declaring a dependency unused at the workspace level.
- Do not propose deleting public exports, registry entries, or generated artifacts at `HIGH` risk without direct evidence.
- Do not modify code unless the user explicitly asks for cleanup after the audit.
- State which checks could not be run and why.
