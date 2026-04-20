---
title: Agentic Coding
type: concept
tags: [llm, agents, coding, benchmarks]
created: 2026-04-20
updated: 2026-04-20
sources: [https://qwen.ai/blog?id=qwen3.6-max-preview]
---

# Agentic Coding

The capability of an LLM to autonomously complete multi-step software engineering tasks — writing, executing, debugging, and iterating on code with minimal human intervention. Distinct from single-turn code generation.

## Common Benchmarks
- **SWE-bench Pro** — real-world GitHub issue resolution
- **Terminal-Bench 2.0** — terminal/shell task completion
- **SkillsBench** — breadth of coding skill coverage
- **SciCode** — scientific coding tasks
- **NL2Repo** — natural language to repository-level code
- **QwenClawBench / QwenWebBench** — Qwen-specific agent evals

## Key Techniques
- **`preserve_thinking`** — carry reasoning traces across turns so the model retains context in long agentic loops (used in [[Qwen3.6-Max-Preview]])

## Related
- [[Qwen3.6-Max-Preview]]
