---
name: agent-token-budget
description: Use when an AI agent is consuming too many tokens, costs are spiraling, output is bloated with narration/re-reading, or before running expensive multi-step agent workflows — to set a token budget and curb waste.
version: 1.0.0
---

# Agent Token-Budget & Cost Control

## Overview

Agentswaste tokens at an alarming rate. Top reported cost problems in 2026 (Reddit r/AI_Agents, r/theprimeagen): agents **narrate their reasoning aloud**, **re-read the whole repo into context every turn**, and **re-do work** — turning a $0.02 task into $2. The pain: *"When AI tokens start costing more than your actual employees."*

**Core principle: tokens are money. Give the agent an explicit budget, cap context reads, and strip narration from output.**

## When to Use

Use this skill when:
- An agent's token burn feels too high / costs are climbing with no clarity on what's driving it
- The agent re-reads files/repo repeatedly into context
- The agent "thinks out loud" in verbose narration, logs, or self-talk
- You run many agent calls in a batch or a long multi-step workflow
- You want to predict/limit how much a run will cost before spending

**Do NOT use for**: single cheap one-off calls (micromanagement adds overhead).

## Core Budget Pattern

```
1. SET A HARD BUDGET        → max tokens per run & max $ (stop when exceeded)
2. LIMIT CONTEXT READS      → only fetch what's needed, no full-repo dumps
3. SUPPRESS NARRATION       → instruct output strips reasoning self-talk
4. MEASURE & LOG            → track tokens/cost per step; spot the burners
5. COMPRESS BEFORE REPEAT   → summarize prior context instead of re-sending raw
```

## Quick Reference

| Action | Move |
|--------|------|
| Cap total spend | `max_tokens_per_run`, `max_cost_usd` — stop and ask when hit |
| Stop repo re-reads | Pin files: only read changed/needed files, use diff/incremental context |
| Kill narration | Output contract: "return only the result; no commentary, no thinking-out-loud" |
| Cut re-do waste | Verify-once-then-proceed; don't re-run unchanged steps |
| Long sessions | Summarize context after N turns instead of appending raw history |
| Cost visibility | Log tokens per call; sum; report where budget went |

## Implementation Pattern

Most agent frameworks expose token/cost limits. Set them *before* launching:

```
# Pseudocode — apply at the API/framework layer
run(
    input=task,
    model=model,
    max_tokens=budget.total_tokens,     # hard ceiling
    cost_limit=budget.cost_usd,         # stop & notify when exceeded
    context=trimmed_context,            # only needed files, not whole repo
    system="Return only the deliverable. No narration, no reasoning self-talk,"
           " no 'Here is what I did' preamble.",
)
```

Framework-level knobs to prefer (CSS-over-JS principle — use built-in limits before building custom logic):
- OpenAI/Anthropic: `max_tokens`, `max_tokens_to_sample` + prompt caching
- vLLM / serving layers: `--max-model-len`, request budgets
- CLI agent memory windows: set workspace `max_context` / token cap

## Common Mistakes

- **No budget set** → a runaway loop spends more than the whole feature budget.
- **Full-context reload every turn** → most expensive single pattern; cap it.
- **Narration tokens** → agents add 30-50% overhead narrating; strip it in the system prompt.
- **Not measuring** → can't fix what you don't see; always log per-call tokens.
- **Re-running unchanged steps** → verify once, don't re-read the world each loop.

## Red Flags — STOP and Trim

- No `max_tokens`/cost ceiling on a long or batch run
- Agent reads the entire repo/files into context on every turn
- Output streams with lengthy reasoning/logging before the actual answer
- Cost climbing with no log of which calls did it

**Any of these: set a hard budget, trim context to essentials, suppress narration, log tokens — then the run is controllable.**

## Real-World Impact

- #2 pain point (Woche 2026-08-07, 21/30): "My agent is too damn expensive", "How do I reduce token consumption" — r/AI_Agents
- r/theprimeagen: "When AI tokens start costing more than your actual employees"
