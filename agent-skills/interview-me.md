---
name: interview-me
description: Extract the user's real intent before planning, specifying, or coding. Use when an ask is underspecified, conventional, or missing who it is for, why it matters now, what success looks like, or the binding constraint; when the user says "interview me", "grill me", "are we sure?", "stress-test my thinking", or similar; or when Codex catches itself silently filling in ambiguous requirements before any plan, spec, or code exists.
---

# Interview Me

## Purpose

Use this skill to find the gap between what the user asked for and what they actually want before switching costs exist. The deliverable is a confirmed statement of intent, not a plan, spec, task list, or implementation.

Do not use this skill for clear mechanical requests, pure explanations, or cases where the user explicitly prioritizes speed over verification. Do not use it in non-interactive contexts such as scheduled runs, CI, `/loop`, or autonomous loops; instead, state that clarification is blocked on live user input.

## Interview Loop

### 1. Start With A Hypothesis

Before asking anything, state one sentence describing your current best read of the user's intent and give an honest confidence number.

```text
HYPOTHESIS: You want a way to answer "how are we doing?" in standup, and "dashboard" was the conventional artifact that came to mind.
CONFIDENCE: ~30% - missing: who it is for, what metrics means here, and what success looks like.
```

If confidence is below about 70%, include the reason on the same line: what is unresolved or missing.

### 2. Ask One Question At A Time

Ask exactly one focused question, and attach your best guess plus the reasoning that produced it.

```text
Q: When you say "how are we doing?", who is asking: you, the team, or someone up the chain?
GUESS: The engineering team in standup, because "we" usually scopes that way. If it is for execs, the metrics and framing change a lot.
```

Wait for the user before asking the next question. Do not batch questions. The next question should depend on the prior answer.

### 3. Probe "Want" Versus "Should Want"

Treat best-practice language as a warning sign when it lacks a concrete outcome: "scalable", "clean", "modern", "robust", "standard", "good engineering practice", "I should probably...".

When that happens, ask:

```text
If you did not have to justify this to anyone, what would you actually want?
```

Be visibly willing to be wrong. A wrong guess is useful because the user can correct it faster than they can invent an answer from scratch.

### 4. Stop At 95% Confidence

Continue until you can answer yes to:

```text
Can I predict the user's reaction to the next three questions I would ask?
```

If yes, stop interviewing and restate the intent. If several rounds pass without your confidence rising, stop and say:

```text
I have asked X questions and still cannot predict your reactions. Something foundational is missing. Want to step back?
```

## Restate And Confirm

When confidence is high, restate the intent in 5-8 tight lines using the user's language where practical:

```text
Here is what I now think you want:

- Outcome:      <one line>
- User:         <one line - who benefits>
- Why now:      <one line - what changed>
- Success:      <one line - how we know it worked>
- Constraint:   <one line - the binding limit>
- Out of scope: <one line - what we are explicitly not doing>

Yes / no / refine?
```

The `Out of scope` line is mandatory.

Require an explicit yes before moving to downstream work. Do not accept "whatever you think", "sounds good", "sure, let's go", silence, or "okay let's start" as final confirmation. For vague agreement, ask what they would refine. For delegation, give two concrete choices and ask them to choose.

If the user corrects the restate, fold in the correction and restate again.

## Handoffs

After explicit confirmation, hand off only from the confirmed intent:

- Use idea refinement when the user wants options for how to satisfy the intent.
- Use specification or planning skills when the intent is concrete enough to write down.
- If the user wants persistence for a multi-session project or handoff, offer to save the confirmed intent to `docs/intent/[topic].md`; save only after they confirm.

## Red Flags

- Asking three or more questions in one message.
- Asking a question without a guess.
- Producing a spec, plan, task list, or code before confirmed intent.
- Treating sophistication-signaling words as goals.
- Accepting "whatever you think" as a decision.
- Letting confidence stay below 70% without naming what is missing.
- Skipping the `Out of scope` line.
- Saving an intent document before explicit confirmation.

## Verification

Before leaving this skill, verify:

- The first turn included a hypothesis and confidence number.
- Each question was one-at-a-time and included a guess.
- Low confidence included a reason.
- Any convention-signaling or sophistication-signaling answer was probed.
- The final restate included Outcome, User, Why now, Success, Constraint, and Out of scope.
- The user gave an explicit yes.