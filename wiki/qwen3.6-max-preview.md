---
title: Qwen3.6-Max-Preview
type: summary
tags: [llm, qwen, alibaba, agentic-coding, proprietary-model]
created: 2026-04-20
updated: 2026-04-20
sources: [https://qwen.ai/blog?id=qwen3.6-max-preview]
---

# Qwen3.6-Max-Preview

An early preview of [[Qwen Team]]'s next proprietary model, released 2026-04-17. Positioned as a step above [[Qwen3.6-Plus]], with improvements concentrated in agentic coding, world knowledge, and instruction following. Still under active development at time of publication.

## Key Improvements over Qwen3.6-Plus

| Area | Benchmark | Delta |
|------|-----------|-------|
| Agentic Coding | SkillsBench | +9.9 |
| Agentic Coding | SciCode | +6.3 |
| Agentic Coding | NL2Repo | +5.0 |
| Agentic Coding | Terminal-Bench 2.0 | +3.8 |
| World Knowledge | QwenChineseBench | +5.3 |
| World Knowledge | SuperGPQA | +2.3 |
| Instruction Following | ToolcallFormatIFBench | +2.8 |

Claims top score on six major coding benchmarks: SWE-bench Pro, Terminal-Bench 2.0, SkillsBench, QwenClawBench, QwenWebBench, and SciCode.

## Access

- **Chat UI:** [Qwen Studio](https://chat.qwen.ai/)
- **API:** `qwen3.6-max-preview` via [[Alibaba Cloud Model Studio]] (OpenAI-compatible and Anthropic-compatible endpoints)

## Notable Feature: `preserve_thinking`

Supports `preserve_thinking` in the API — preserves reasoning/chain-of-thought content from prior turns in the message history. Recommended for [[Agentic Coding]] workflows where multi-step reasoning continuity matters.

## API Regions (DashScope)

- Beijing: `dashscope.aliyuncs.com/compatible-mode/v1`
- Singapore: `dashscope-intl.aliyuncs.com/compatible-mode/v1`
- US (Virginia): `dashscope-us.aliyuncs.com/compatible-mode/v1`

## Related
- [[Qwen Team]]
- [[Alibaba Cloud Model Studio]]
- [[Agentic Coding]]
