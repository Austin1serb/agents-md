# How to Change Codex System Prompt

Codex has a built-in instruction layer, but you can replace it with your own system prompt using `model_instructions_file` in your Codex config.

This is useful when you want Codex to behave less like a generic coding assistant and more like a consistent coding agent inside your workspace.

## Adding a Custom System Prompt to Codex

Create a markdown file for your custom Codex instructions.

Example:

```txt
codex-optimized-prompt.md
```

Then point your Codex config to that file from your `.codex/config.toml`:

```toml
model_instructions_file = "path/to/codex-optimized-prompt.md"
```

OpenAI's Codex config reference describes `model_instructions_file` as a replacement for Codex's built-in instructions. It also supports profile-scoped (CLI only) replacement instruction files with `profiles.<name>.model_instructions_file`. 

Official Openai docs:
[https://developers.openai.com/codex/config-reference](https://developers.openai.com/codex/config-reference#:~:text=the%20active%20model.-,model_instructions_file,-string%20(path))

## Custom Codex Instructions vs [AGENTS.md](./AGENTS.md)

`model_instructions_file` and `AGENTS.md` are different instruction layers.

An LLM goes through these layers in order:

1. Openai's hidden system prompt (built-in instructions)
2. `model_instructions_file`
3. `AGENTS.md` (Developer Prompt)
4. The `user` message for the current turn of the conversation.

The instructions of the user cannot override the instructions of the AGENTS, and the AGENTS.md cannot override the instructions of the `model_instructions_file`. The `model_instructions_file` cannot override the instructions of the OpenAI system prompt. Each layer is separate and has its own level of authority.

The `model_instructions_file` is a system prompt that we have control over. This is a extremely important file, it defines the highest-level rules for how Codex should behave overall, and how to think, act and respond in general.

`AGENTS.md` is a developer prompt that we have control over. This is also an important file, but it is more focused on the specific agents and subagents that we have defined, and how they should behave in relation to each other. You could technically put all your instructions in the `model_instructions_file` and leave `AGENTS.md` blank, and get close to the same responses. But it's better to use `model_instructions_file` for the high-level rules and preferences, and `AGENTS.md` for the specific agent definitions and instructions.

## Add a Custom System Prompt for Subagents

You can also use different instruction files for Codex subagents.

For example, your default Codex agent can use a coding-focused prompt, while a copywriting profile can use a writing-focused prompt.

Example:

copywriter.toml:

```toml
description = "Writes website copy, messaging, and conversion-focused UX copy."
model_instructions_file = "../copywriter_instructions.md"
```

This will completely change the default behavior for that subagent, instead of it thinking and acting like a coding assistant, it will think and act like a copywriter. (assuming your `copywriter_instructions.md` is good).

This repo includes Codex' base system prompt here:

[`codex-GPT-5.5-system-prompt.md`](./codex-GPT-5.5-system-prompt.md)

As well as an optimized system prompt for coding agents here:

[`codex-optimized-prompt.md`](./codex-optimized-prompt.md)
