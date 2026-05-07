# AGENTS.md Patterns for Context Engineering in Coding Agents

Practical AGENTS.md prompt patterns for Codex, Claude Code, Cursor, Windsurf, GitHub Copilot, and other coding agents.

This repo focuses on context engineering: reducing token waste, protecting the context window, avoiding huge command-output dumps, and improving coding-agent reliability.

> There will be more to come, follow or watch to get updates!

## Biggest win: byte-capped command output

Line limits like `head -n 20`, `tail -n 20`, or `sed -n '1,20p'` can still flood the context window when output contains one huge line. This can overload the agents context window with unrelated information, thus reducing the quality of the response while increasing cost.

Safer default:

```bash
COMMAND 2>&1 | head -c 4000
```

For logs or recent failures:

```bash
COMMAND 2>&1 | tail -c 4000
```

In my own coding-agent workflows, this one AGENTS.md rule reduced average token usage by roughly 50% across comparable tasks.

## What this AGENTS.md covers

- command-output byte caps
- context window protection
- token efficiency
- scoped search discipline
- validation rules
- prompt-injection resistance
- minimal code-change behavior
- coding-agent communication rules

## Why this matters

Coding agents usually know how to run commands.

The missing behavior is context discipline.

This AGENTS.md teaches agents to inspect scope before printing content, cap unknown output by bytes, preserve useful context, and narrow commands instead of dumping large files, logs, diffs, or search results.

## Main file

See [`AGENTS.md`](./AGENTS.md).

## Related tools

These patterns are written for AGENTS.md, but many can be adapted for:

- Codex
- Claude Code
- Cursor rules
- Windsurf rules
- GitHub Copilot instructions
- custom AI coding agents

Built by [Austin Serb](https://austinserb.com).
