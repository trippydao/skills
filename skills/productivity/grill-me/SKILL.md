---
name: grill-me
description: A relentless interview to sharpen a plan or design.
disable-model-invocation: true
---

Interview me relentlessly about every aspect of this plan until we reach a shared understanding. Walk down each branch of the design tree, resolving dependencies between decisions one-by-one. For each question, provide your recommended answer.

Ask the questions one at a time.

If a question can be answered by exploring the codebase or checking existing system state — cron jobs, scripts, cache files, config, position data — do that instead of asking the user. Before posing a decision question, ask: does the system already know the answer? Check cron job prompts, script outputs, cache files, and existing configs. Only ask the user when the answer genuinely requires their judgment or preference.

When the plan involves system constraints (capacity limits, char caps, rate limits, configurable thresholds), proactively explain the constraint mechanism before asking the first decision question. The user needs to understand the system's rules to make informed decisions — don't make them ask "how does X work?" before they can answer your question. Present the mechanism as part of the initial assessment.

## Execution-phase step tracking

After the grilling resolves all branches and execution begins, the user may lose track of progress through a multi-step plan. To prevent this:

- **Before first execution**, state the current step clearly: "Step 1 of N: ..."
- **After each completed step**, announce completion + next step: "✓ Done. Step 2 of N: ..."
- **If a step has sub-steps**, use the same pattern recursively: "Step 2a of 2: generating token..."
- **When the user asks "what step are we at"** — that's a signal the tracking wasn't clear enough. Re-state the full remaining flow concisely.

This is especially important when steps span multiple message turns or involve waiting for the user to act (e.g., running a terminal command on their machine).
