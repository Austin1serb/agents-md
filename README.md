# AGENTS.md Patterns for Context Engineering in Coding Agents

Practical `AGENTS.md` and Codex prompt patterns for coding agents that need better context discipline, safer command output, and lower token usage.

This repo is for Software Engineers using Codex, Claude Code, Cursor, Windsurf, GitHub Copilot, or custom AI coding agents who want agents to get the most from their agent harness.

> [!NOTE]
> There will be more to come. Follow or watch to get updates.

## What's In This Repo:

| Resource | Purpose |
|---|---|
| [AGENTS.md instructions for coding agents](./AGENTS.md) | Optimized coding-agent instructions for context discipline, and better responses. |
| [Coding-optimized system prompt](./codex-optimized-prompt.md) | A practical Codex prompt more focued on coding. |
| [How to change Codex system prompt](./change-codex-system-prompt.md) | Instructions for replacing Codex system prompt, including subagent instruction files. |
| [OpenAI Codex GPT-5.5 base system prompt](./codex-GPT-5.5-system-prompt.md) | OpenAI's base Codex GPT-5.5 system prompt, which is more general-purpose than the coding-optimized prompt. |

## Biggest Current Win: Byte-capped command output

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

see: [AGENTS.md](https://github.com/Austin1serb/agents-md/blob/main/AGENTS.md#command-output) - Command Output

In my own Codex workflows, this single `AGENTS.md` rule reduced average token usage by roughly 50% across comparable tasks.

## Why Context Discipline Matters

Coding agents are great at writing shell commands, but often consume much more information than necessary to complete a task. For example, you might have a file that contains many utility functions, you might ask the agent to find a specific function and explain it. The agent might read the entire file, when it only needed to read a few lines to find the function definition. This can lead to degraded responses, higher token usage, and more irrelevant information in context.

## How to Use AGENTS.md

Copy [`AGENTS.md`](./AGENTS.md) into the root of any repo that supports agent instruction files. To use in all repos, add it to the root of `/.codex`

For Codex, this repo also includes [`codex-optimized-prompt.md`](./codex-optimized-prompt.md), which I use as a coding-optimized system prompt.

To use it as your default Codex instruction file, download the file, and add this to your `.codex/config.toml`:

```toml
model_instructions_file = "path/to/codex-optimized-prompt.md"
```

You can also set different instruction files for different Codex profiles or subagents.

Built by [Austin Serb](https://austinserb.com).
