# AGENTS.md Patterns for Context Engineering in Coding Agents

Practical `AGENTS.md` and Codex prompt patterns for coding agents that need better context discipline, safer command output, and lower token usage.

This repo is for Software Engineers using Codex, Claude Code, Cursor, Windsurf, GitHub Copilot, or custom AI coding agents who want agents to get the most from their agent harness.

> [!NOTE]
> There will be more to come. Follow or watch to get updates.

## What is in this repo

| File | Purpose |
|---|---|
| [`AGENTS.md`](./AGENTS.md) | Optimized Coding-agent instructions for context discipline, command-output byte caps, scoped search, validation, and safe code changes. |
| [`codex-optimized-prompt.md`](./codex-optimized-prompt.md) | A coding-optimized Codex system prompt for stronger default behavior across tasks. |
| [`change-codex-system-prompt.md`](./change-codex-system-prompt.md) | How to replace the Codex system prompt with `model_instructions_file`, including subagent instruction files. |
| [`codex-GPT-5.5-system-prompt.md`](./codex-GPT-5.5-system-prompt.md) | OpenAI's base system prompt for Codex GPT-5.5, which is more general-purpose than `codex-optimized-prompt.md`. |

## Biggest current win: Byte-capped command output

A common coding-agent failure mode is pulling thousands of irrelevant lines into context while researching a task.

Line limits like `head -n 20`, help sometimes, but they are not safe. One huge line can still flood the context window, reducing the output quality and increasing token usage.

Use byte caps for unknown or potentially large command output:

```bash
COMMAND 2>&1 | head -c 4000
```

For logs, test failures, or recent output:

```bash
COMMAND 2>&1 | tail -c 4000
```

In my own Codex workflows, this single `AGENTS.md` rule reduced average token usage by roughly 50% across comparable tasks.

## Why context discipline matters

Coding agents are good at writing shell commands, but I have found they often consume much more information than necessary to complete a task. For example, you might have a file that contains many utility functions, and you ask the agent to find a specific function and explain it. The Agent might read the entire file, when it only needed to read a few lines to find the function definition. This can lead to degraded responses, higher token usage, and more irrelevant information in the context.

## How to use AGENTS.md

Copy [`AGENTS.md`](./AGENTS.md) into the root of a repo that supports agent instruction files.

For Codex, this repo also includes [`codex-optimized-prompt.md`](./codex-optimized-prompt.md), which I use as a coding-optimized system prompt.

To use it as your default Codex instruction file, download the file, and add this to your `.codex/config.toml`:

```toml
model_instructions_file = "path/to/codex-optimized-prompt.md"
```

You can also set different instruction files for different Codex profiles or subagents.

Built by [Austin Serb](https://austinserb.com).