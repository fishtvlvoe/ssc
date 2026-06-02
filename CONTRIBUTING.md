# Contributing

Thanks for considering a contribution to SSC.

SSC is small by design. Changes should keep the workflow easy to inspect and
safe for maintainers to run inside any AI coding agent.

## Good Contributions

- Improve the Skill / Agent / Hook classification rules.
- Add clearer examples for edge cases.
- Improve Gen-3 quality checks.
- Tighten Hook safety guidance.
- Fix documentation that is unclear, outdated, or hard to follow.

## Development Rules

- Keep `SKILL.md` focused on the main workflow.
- Move long reference material into `knowledge/`.
- Prefer concrete examples over abstract explanation.
- Do not add secrets, local machine paths, or private project details.
- Keep generated automation safe by default, especially Hooks.

## Pull Request Checklist

- [ ] The change has a clear maintainer use case.
- [ ] `README.md` still matches the actual behavior.
- [ ] `knowledge/templates.md` and `knowledge/quality-check.md` stay consistent.
- [ ] Hook-related changes mention timeout and failure behavior.
- [ ] The version or changelog is updated when behavior changes.
