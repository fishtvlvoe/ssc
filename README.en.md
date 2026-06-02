# SSC — Super Skills Creator

> English | **[繁體中文](README.md)**

**Current version:** v1.2.0

SSC is a skill for AI coding agents — turning repeated workflows into reusable
project assets: **Skills**, **Agents**, and **Hooks**.

Works with any agent that supports skill loading:
**Claude Code** · **Codex** · **OpenAI Codex CLI** · and others.

It answers a practical question:

> Should this workflow become an interactive Skill, an autonomous Agent, or an
> event-driven Hook?

SSC guides you through classification, interview questions, file structure,
templates, and quality checks so the result is not just another prompt, but a
reusable automation unit.

---

## Why This Exists

AI coding workflows often start as one-off prompts. That works once, but it
does not scale across a team, a repo, or repeated maintenance work.

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

SSC uses a Gen-3 standard for maintainable AI agent skills.

Every generated Skill should include:

| Requirement | Why it matters |
|-------------|----------------|
| Execution metadata | Declares invocation mode so the agent loads the skill correctly |
| GATE alignment | Confirms the user intent before work begins |
| Hard stop points | Prevents the agent from making hidden product decisions |
| Quality checks | Makes completion testable instead of subjective |
| Completion checklist | Gives maintainers a clear done/not-done boundary |

Agents and Hooks have their own checks:

- **Agents** must have a single responsibility, checklist-driven review, and
  structured output.
- **Hooks** must be event-correct, executable, bounded by timeout, and safe on
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
| `SKILL.md` | Main SSC workflow loaded by the AI agent |
| `knowledge/classification.md` | Decision tree for Skill vs Agent vs Hook |
| `knowledge/templates.md` | Output templates and structure rules |
| `knowledge/quality-check.md` | Validation rules for generated assets |
| `CHANGELOG.md` | Release history |
| `VERSION` | Current release version |

---

## Installation

### Claude Code

```bash
cd ~/.claude/skills
git clone https://github.com/fishtvlvoe/ssc.git ssc
```

Restart Claude Code, then invoke with `/ssc`.

### Codex CLI

```bash
cd ~/.codex/skills      # or your Codex skills directory
git clone https://github.com/fishtvlvoe/ssc.git ssc
```

### Other Agents

Copy the `SKILL.md` and `knowledge/` folder into wherever your agent loads
skills from. The only requirement is that the agent can read markdown files
and follow the workflow instructions inside.

### Invocation

Once installed, trigger SSC with `/ssc` or natural language:

- build a skill
- create an agent
- add a hook
- upgrade this skill
- turn this workflow into a reusable skill

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

Useful contributions include:

- Reviewing pull requests that change the decision tree or templates
- Generating regression examples for Skill / Agent / Hook classification
- Checking generated skills against the Gen-3 quality standard
- Improving release notes and documentation
- Reviewing security implications of generated Hooks

---

## License

MIT. See [LICENSE](LICENSE).

---

Built and maintained by [@fishtvlvoe](https://github.com/fishtvlvoe).
