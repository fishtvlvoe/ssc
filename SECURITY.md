# Security Policy

SSC helps generate Skills, Agents, and Hooks for AI coding agents. Hooks are the
highest risk output because they execute shell commands from agent events.

## Supported Versions

| Version | Supported |
|---------|-----------|
| v1.2.x | Yes |
| v1.1.x | Best effort |
| v1.0.x | No |

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
