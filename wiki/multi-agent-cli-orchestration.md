---
title: Multi-Agent CLI Orchestration
type: concept
tags: [multi-agent, cli, workflow, llm, orchestration]
created: 2026-04-20
updated: 2026-04-20
sources: [https://juanpabloaj.com/2026/04/16/a-lightweight-way-to-make-agents-talk-without-paying-for-api-usage/]
---

# Multi-Agent CLI Orchestration

A class of [[Agentic Coding]] workflow where multiple LLM agents (potentially from different vendors) coordinate via CLI invocations rather than through an API orchestration framework. The key insight: subscription-tier CLIs already support session persistence, so agents can hand off work by invoking each other's CLIs and resuming previous sessions.

## Why Cross-Vendor

Using multiple vendors provides genuinely different model perspectives rather than just another pass from the same model family. A single vendor's subagent system may share weights, training data, and biases — an external reviewer from a different lab is more likely to catch different failure modes.

## Two Approaches

| Approach | Tool | Best for |
|----------|------|---------|
| Non-interactive resume | CLI flags (`--last`, `-r latest`) | Minimal setup, fast experimentation |
| tmux panes + sockets | tmux | Visibility, parallel agents, debugging |

See [[Lightweight Multi-Agent CLI Orchestration]] for concrete commands.

## Known Limitations

- **Visibility gap** (non-interactive): hard to inspect what happened at each step
- **Polished hallucination risk**: agents can converge to fluent consensus that is still wrong; more iterations ≠ more correct
- **Permission surface**: autonomous agent-to-agent invocations expand the permission footprint — needs attention
- **Not a framework**: this pattern trades observability for simplicity; not suitable for production pipelines requiring audit trails

## Related
- [[Agentic Coding]]
- [[Lightweight Multi-Agent CLI Orchestration]]
