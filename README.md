# LLM Latency Benchmark

AIMultiple benchmark of 11 large language models on short-answer Q&A and long-answer code generation. The study measures first-token latency, per-token latency and end-to-end response time, and reports reasoning and non-reasoning models separately.

> [Read the benchmark on AIMultiple](https://aimultiple.com/llm-latency-benchmark)

## Workload

The set combines the five most-used models on OpenRouter with six other current models. Claude Opus 4.8, Claude Opus 4.7, Claude Sonnet 5, Claude Haiku 4.5 and GPT-5.2 are non-reasoning by default. DeepSeek V4 Flash, Xiaomi MiMo v2.5, MiniMax M3, Gemini 3.1 Pro, Tencent Hunyuan HY3 and Claude Fable 5 reason by default.

Each use case has 20 prompts, sent 3 times per model, for 1,320 requests in total. Output is capped at 128 tokens for Q&A and 1,024 for coding, and reasoning models get extra budget for thinking. The client streamed every response from a single region, with a unique text block in each prompt to prevent caching. Each model ran on one pinned provider. The article reports median (p50) and p90 values.

## Benchmark results

On Q&A, the first answer token arrived in 0.75 seconds for claude-opus-4-8 and in 1.2 to 14.6 seconds for reasoning models. On code generation, end-to-end time ran from about 5.5 seconds for claude-haiku-4-5 to 35 seconds for mimo-v2-5.

GPT-5.2 reasoned on 62% of coding requests and on no Q&A requests. Its p90 rose from under 2 seconds on Q&A to about 11 seconds on coding.

## Scope

Results reflect default model settings, one provider per model and a client in Europe. The endpoint also matters: Claude Opus 4.8 on Google Vertex (Europe) returned its first token in about 0.75 seconds, while Claude Opus 4.7 on Anthropic's own API took about 2 seconds, although the two are different versions.

## Ownership

The benchmark implementation was developed for AIMultiple and belongs to AIMultiple. This repository contains a documentation summary. Source code and benchmark datasets are not distributed here.
