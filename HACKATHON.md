# Team Unify

## Members

| Name | Role |
|---|---|
| Aryan Mudgal | Team Lead |
| Chandarsekhar Panda | Member |

## Problem

**Problem 06: Open Source Decision Intelligence and Knowledge Recovery**

Open-source projects accumulate years of technical discussions across GitHub issues, pull requests, review threads, forums, and design documents. Important architectural decisions are made in these discussions but are rarely documented. When experienced contributors leave, the reasoning behind those decisions is lost, and new contributors may repeat rejected approaches or introduce incompatible changes.

Our system recovers this knowledge. It:

- Analyzes public discussions, issues, pull requests, and technical threads
- Extracts decisions and the reasoning behind them
- Identifies rejected alternatives and explains why they were rejected
- Links decisions to the relevant source code, even after files are renamed or moved
- Keeps a reference to the original discussion for every decision
- Surfaces relevant historical decisions when a new pull request modifies associated code
- Preserves traceability so maintainers can verify every extracted decision

## Open-Source Models and Why We Use Them

| Model | Where we use it | Why this model |
|---|---|---|
| **Gemma** | Pre-filtering. Classifies each post in a discussion as decision-bearing or not, and tags its stance (proposal, objection, or agreement). | Small and fast, so it can run locally over thousands of posts cheaply and keep noise away from the larger models. |
| **Qwen** | Structured extraction of decisions, rationale, and alternatives as JSON. Embeddings and reranking to match decisions to code and to new pull requests. | Reliable structured output, long-context handling for big threads, and strong embedding and reranker models from the same family. |
| **DeepSeek** | Deciding which approaches were accepted and which were rejected, and generating the reasons for each rejection. | Multi-step reasoning is needed to follow a debate across many posts and infer implicit rejections, which is the core of the evaluation. |

## How the Models Fit Together

1. **Gemma** filters the raw discussion down to the posts that matter.
2. **Qwen** extracts structured decisions and retrieves related code and past decisions.
3. **DeepSeek** reasons over the extracted material to separate accepted from rejected approaches and explain why.

Every decision keeps a quoted source span and a link to the original post, so it can be verified without trusting the model.

## Development Tools

- **IDE:** Antigravity IDE
