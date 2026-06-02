# Security Policy

SSC helps generate Claude Code Skills, Agents, and Hooks. Hooks are the highest
risk output because they execute shell commands from Claude Code events.

## Supported Versions

| Version | Supported |
|---------|-----------|
| v1.1.x | Yes |
| v1.0.x | Best effort |

## Reporting a Vulnerability

Please open a GitHub issue with:

- affected file or template
- expected safe behavior
- actual risky behavior
- a minimal reproduction or example

Do not include secrets, API keys, tokens, or private project data in the issue.

## Security Focus Areas

- unsafe Hook command templates
- missing timeout guidance
- generated automation that can block or damage a workflow
- prompts that encourage leaking secrets or private file paths
- unclear permission boundaries between Skill, Agent, and Hook outputs
