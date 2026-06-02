# SSC — Super Skills Creator

**Current version:** v1.2.0

SSC is a Claude Code skill for turning repeated AI coding workflows into reusable
project assets: **Skills**, **Agents**, and **Hooks**.

It answers a practical maintainer question:

> Should this workflow become an interactive Skill, an autonomous Agent, or an
> event-driven Hook?

SSC then guides the maintainer through classification, interview questions,
file structure, templates, and quality checks so the result is not just another
prompt, but a reusable automation unit.

---

## Why This Exists

AI coding workflows often start as one-off prompts. That works once, but it does
not scale across a team, a repo, or repeated maintenance work.

SSC helps convert those workflows into maintainable structure:

| Need | SSC Output | Example |
|------|------------|---------|
| Human-in-the-loop workflow | Skill | Planning, debugging, writing, deployment runbook |
| Independent expert task | Agent | Code review, security review, repo analysis |
| Event-triggered automation | Hook | Session setup, guardrails, logging, pre-tool checks |

The goal is simple: make AI-assisted development workflows reviewable,
versioned, reusable, and easier to improve.

---

## What SSC Does

SSC supports three operating modes:

| Mode | Purpose |
|------|---------|
| New | Build a Skill, Agent, or Hook from scratch |
| Convert | Adapt an existing skill or prompt into the SSC structure |
| Upgrade | Bring an older Gen-1 / Gen-2 workflow up to the Gen-3 standard |

The workflow:

```text
GATE alignment
  -> classify Skill / Agent / Hook
  -> collect requirements
  -> generate structure
  -> run quality checks
  -> confirm completion
```

---

## Generation 3 Standard

SSC uses a Gen-3 standard for maintainable Claude Code skills.

Every generated Skill should include:

| Requirement | Why it matters |
|-------------|----------------|
| Execution metadata | Declares invocation mode so Claude Code loads the skill correctly |
| GATE alignment | Confirms the user intent before work begins |
| Hard stop points | Prevents the agent from making hidden product decisions |
| Quality checks | Makes completion testable instead of subjective |
| Completion checklist | Gives maintainers a clear done/not-done boundary |

Agents and Hooks have their own checks:

- Agents must have a single responsibility, checklist-driven review, and
  structured output.
- Hooks must be event-correct, executable, bounded by timeout, and safe on
  failure.

---

## Repository Structure

```text
ssc/
├── SKILL.md
├── VERSION
├── CHANGELOG.md
├── CONTRIBUTING.md
├── SECURITY.md
└── knowledge/
    ├── classification.md
    ├── templates.md
    └── quality-check.md
```

| File | Role |
|------|------|
| `SKILL.md` | Main SSC workflow loaded by Claude Code |
| `knowledge/classification.md` | Decision tree for Skill vs Agent vs Hook |
| `knowledge/templates.md` | Output templates and structure rules |
| `knowledge/quality-check.md` | Validation rules for generated assets |
| `CHANGELOG.md` | Release history |
| `VERSION` | Current release version |

---

## Installation

Clone SSC into your Claude Code skills directory:

```bash
cd ~/.claude/skills
git clone https://github.com/fishtvlvoe/ssc.git ssc
```

Restart Claude Code, then invoke:

```text
/ssc
```

You can also trigger it naturally with phrases such as:

- build a skill
- create an agent
- add a hook
- upgrade this skill
- turn this workflow into a reusable Claude Code skill

---

## Example Use Cases

| Scenario | Recommended Output |
|----------|--------------------|
| A repeated deployment checklist with user confirmations | Skill |
| A code review process that can run independently | Agent |
| A rule that blocks dangerous shell commands before execution | Hook |
| A long prompt that your team keeps copying between projects | Skill |
| A repo analyzer that reads files and reports risks | Agent |

---

## Maintainer Notes

SSC is maintained as an open-source workflow tool for AI-assisted software
maintenance. It is intentionally small: the main workflow stays readable, while
larger reference material lives in `knowledge/` and is loaded only when needed.

Useful maintenance work for Codex includes:

- reviewing pull requests that change the decision tree or templates
- generating regression examples for Skill / Agent / Hook classification
- checking generated skills against the Gen-3 quality standard
- improving release notes and documentation
- reviewing security implications of generated Hooks

---

## License

MIT. See [LICENSE](LICENSE).

---

Built and maintained by [@fishtvlvoe](https://github.com/fishtvlvoe).
