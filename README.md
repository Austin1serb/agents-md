# Agent Prompts

Practical prompt files for coding agents.

The current focus is context discipline: reducing token waste, avoiding large command-output dumps, which reduce the effectiveness of coding agents.

## Main file

See [`AGENTS.md`](./AGENTS.md).

## Biggest current win

The `## Command Output` section is the highest-impact rule so far. It makes coding agents byte-cap unknown command output instead of relying only on line limits.

Line limits like `head -n 20`, `tail -n 20`, and `sed -n '1,20p'` can still flood the context window when output contains a huge single-line file, minified JSON, JSONL record, log entry, or stack trace.

Safer default:

```bash
COMMAND 2>&1 | head -c 4000
```

For recent failures or logs:

```bash
COMMAND 2>&1 | tail -c 4000
```

In my own use, adding this rule to my base `AGENTS.md` reduced average token usage by roughly 50% across comparable coding-agent tasks.

## Philosophy

Agents usually know how to run commands. The missing behavior is context discipline.

These prompts are designed to make agents:

- inspect scope before printing content
- cap unknown output by bytes
- preserve exit codes when validation matters
- avoid broad unbounded searches
- narrow commands instead of dumping more output

Built by [Austin Serb](https://austinserb.com).
