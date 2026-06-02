# Changelog

## v1.2.0 - 2026-06-02

### Changed

- Simplified SKILL.md description to match actual runtime behavior.
- Removed `disable-model-invocation` frontmatter — SSC needs model invocation for GATE and interview steps.
- Updated delegation rules: replaced deprecated `cursor-agent`/`Kimi` references with `Haiku`/`Sonnet` subagents (aligns with routing.md 2026-05-24 update that retired external CLIs).
- Removed GitHub Release prompt from completion checklist (handled externally).

## v1.1.0 - 2026-06-02

### Added

- Added OSS-ready project documentation focused on the real maintainer problem:
  turning repeated AI coding workflows into reusable Skills, Agents, and Hooks.
- Added `VERSION` so the current project version is explicit outside Git tags.
- Added `LICENSE`, `CONTRIBUTING.md`, and `SECURITY.md` for public maintenance.

### Changed

- Rewrote `README.md` to explain SSC's purpose, Gen-3 quality standard,
  repository structure, installation, examples, and maintainer use cases.
- Clarified how Codex can help maintain the project through PR review,
  regression examples, release notes, documentation, and Hook security review.

## v1.0.0 - 2026-04-11

### Added

- Initial SSC skill.
- Classification tree for Skill / Agent / Hook decisions.
- Templates for generating Skills, Agents, and Hooks.
- Quality-check reference for generated workflow assets.
