---
title: Lightweight Multi-Agent CLI Orchestration
type: summary
tags: [multi-agent, cli, claude, codex, gemini, tmux, workflow]
created: 2026-04-20
updated: 2026-04-20
sources: [https://juanpabloaj.com/2026/04/16/a-lightweight-way-to-make-agents-talk-without-paying-for-api-usage/]
---

# Lightweight Multi-Agent CLI Orchestration

Practical pattern for making coding agents collaborate across vendors using only subscription CLIs — no APIs, SDKs, or extra dependencies. Published at juanpabloaj.com (2026-04-16).

Motivation: get different model perspectives (cross-vendor critique) and extend sessions without paying API rates. See [[Multi-Agent CLI Orchestration]] for the general concept.

## Pattern 1: Non-Interactive Resume (Simple)

One agent invokes another via CLI, resuming the previous session so context is preserved:

```bash
codex exec resume --last "prompt"   # resumes most recent Codex session
gemini -r latest -p "prompt"        # resumes latest Gemini session
```

**Loop:**
1. Agent A produces/reviews a draft
2. Agent A invokes Agent B in resume mode to critique
3. Agent A reads critique, decides next step
4. Repeat until output is stable or discussion stops adding value

**Good for:** minimal setup, no extra dependencies, fast experimentation  
**Limitation:** low visibility — hard to inspect history or monitor progress

## Pattern 2: tmux (Visibility + Parallel)

Agents run in separate tmux panes with a dedicated socket:

```bash
# Create isolated session
SOCKET="${TMPDIR:-/tmp}/claude-tmux-sockets/claude.sock"
mkdir -p "${TMPDIR:-/tmp}/claude-tmux-sockets"
tmux -S "$SOCKET" new -d -s "descriptive-name"

# Send a prompt
tmux -S "$SOCKET" send-keys -t target -l -- "$cmd"
sleep 1
tmux -S "$SOCKET" send-keys -t target Enter

# Capture pane output (no line-wrap artifacts)
tmux -S "$SOCKET" capture-pane -p -J -t target -S -200

# Attach to monitor directly
tmux -S "$SOCKET" attach -t session-name
```

**Good for:** watching interactions live, parallel agents, easier debugging  
**Requires:** tmux installed

## Key Caveat

The author notes an unresolved question: multi-agent consensus is achievable, but it's unclear whether the result is actually better or just a more polished hallucination after a longer chain. LLMs are good at producing plausible text at each step; that doesn't mean the accumulated output is more correct.

Also: pay attention to permissions when one agent is invoking another autonomously.

## Related
- [[Multi-Agent CLI Orchestration]]
- [[Agentic Coding]]
