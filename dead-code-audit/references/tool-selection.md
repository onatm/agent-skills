# Tool Selection

Load only the section for the active stack. Use project-native commands first, then confirm with repository search.

## JavaScript / TypeScript

- Start with `tsc --noEmit`, existing lint scripts, and test commands already defined in `package.json`.
- Use `knip` when present for unused files, exports, and dependencies.
- Use `eslint` rules such as `no-unused-vars` and import-unused checks when configured.
- Use `ts-prune`, `madge`, or bundler dependency graphs only as hints, then verify manually.
- Treat `depcheck` results as low-confidence until confirmed.
- Verify framework conventions such as Next.js routes, Remix loaders, React callbacks, Storybook stories, and registration-by-filename patterns.

## Python

- Start with `ruff check`, `pytest --collect-only`, and the repo's normal test commands.
- Use `vulture` as a hint generator; it often over-reports dynamic usage.
- Check Django, FastAPI, Click, Celery, and pytest discovery paths before marking symbols dead.
- Verify imports referenced through settings modules, entry points, or plugin registries.

## Go

- Start with `go build ./...`, `go test ./...`, and `staticcheck` when available.
- Use `unused` or compiler warnings to find unreachable declarations.
- Use `go mod why` before declaring a module dependency unused.
- Check `init`, interface satisfaction, blank identifier imports, generated mocks, and registration side effects.

## Rust

- Start with `cargo check`, `cargo test`, and existing workspace checks.
- Use compiler `dead_code` warnings and `cargo udeps` when available.
- Verify proc macros, derives, feature-gated code, `serde` bindings, and test-only modules before triaging.
- Treat public crate exports as externally consumable unless the crate is clearly private.

## JVM / .NET

- Start with the repo's normal build and test commands plus existing lint or analyzer tasks.
- Verify DI containers, annotation scanning, reflection, resource loading, and config-based wiring before marking symbols dead.
- Use dependency-analysis plugins only as hints unless the build already enforces them.

## Fallback

- If no specialized tool exists, combine compiler warnings, manifest inspection, and `rg` across source, tests, configs, and build files.
- When tool coverage is partial, keep the finding and lower confidence instead of pretending certainty.
