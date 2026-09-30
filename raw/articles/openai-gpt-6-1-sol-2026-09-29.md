---
source_url: https://openai.com/index/introducing-gpt-6-1-sol/
ingested: 2026-09-30
sha256: 413e4f2aad9955083beafdf46253ee9f498bce7fae4a8ac15451ec187eecc07a
---
# Introducing GPT-6.1 Sol | OpenAI

# GPT-6.1 Sol

## Near-Astra intelligence for a fifth of the price

We’re introducing **GPT‑6.1 Sol**, an upgrade to GPT‑6 Sol that nearly matches GPT‑6 Astra’s intelligence on agentic coding, computer use, and professional work at one-fifth of Astra’s standard input and output token prices. Cached input costs **$0.10 per million tokens**—95% less than standard input pricing and 50% less than GPT‑6 Sol’s cached input pricing—giving developers more room to build and run capable agents that reuse context across requests.

## A more capable Sol across tasks

GPT‑6.1 Sol offers a new balance of capability and cost for important everyday work. It delivers substantial improvements over GPT‑6 Sol across complex professional tasks, from writing and debugging code to understanding documents and executing multi-step business workflows. On several of these evaluations, it approaches GPT‑6 Astra’s performance at substantially lower cost.

### Coding

On **DeepSWE v1.1**, which evaluates complex software-engineering tasks in real codebases, GPT‑6.1 Sol matches GPT‑6 Astra at roughly one-fifth of the cost, while eclipsing GPT‑6 Sol’s best score by 6.4 percentage points at a lower reasoning effort and cost.

DeepSWE 1.1 evaluates AI agents solving original, long-horizon software-engineering tasks.

### Professional work

On **GDP.pdf**, which measures how accurately models answer professional questions using complex PDF documents, including tables, charts, diagrams, and fine-print details, GPT‑6.1 Sol scores higher than Opus 5.5 with fallbacks at less than half the cost per task across the tested reasoning settings. It also approaches GPT‑6 Astra’s state-of-the-art performance at roughly one-fifth the cost per task.

On **AutomationBench**, which measures whether agents correctly complete multi-step business workflows, GPT‑6.1 Sol scores 2.2 percentage points above Opus 5.5 at medium reasoning effort, at roughly a third of the cost. That score is also up 4.8 percentage points from GPT‑6 Sol at the same setting.

### Computer use

On **OSWorld 2.0**’s offline set, which evaluates agents on demanding computer-use workflows, GPT‑6.1 Sol outperforms GPT‑6 Sol by seven percentage points at maximum reasoning effort at less than half the cost. It comes within 2.1 percentage points of Astra’s score at maximum reasoning effort at roughly one-seventh the cost per task.

### Scientific research

On **Terminal-Bench Science 0.1**, which evaluates scientific workflows including data analysis, simulation, and theorem proving, GPT‑6.1 Sol more than doubles GPT‑6 Sol’s score at maximum reasoning effort at less than half the cost per task. At maximum effort, GPT‑6.1 Sol costs $5.47 per task on average, compared with $23.21 for Opus 5.5 and $23.80 for Astra. GPT‑6 Astra still achieves the highest score among the models tested at 68.1% and should be used for the most difficult scientific research tasks.

### Factuality

GPT‑6.1 Sol improves factual accuracy on difficult prompts. At low reasoning effort, the share of responses containing a factual error falls from 11.4% for GPT‑6 Sol to 7.7%. Across the tested reasoning settings, its error rate remains within 1.9 percentage points of GPT‑6 Astra’s at less than one-fifth the cost per task.

This evaluation measures answers to de-identified ChatGPT conversations where users had flagged a prior model’s error. These deliberately difficult prompts are not representative of typical usage.

## Deploying GPT‑6.1 Sol safely

GPT‑6.1 Sol shows substantial improvements over GPT‑6 Sol in OpenAI’s alignment evaluations, bringing it closer to GPT‑6 Astra. OpenAI reports lower failure rates than GPT‑6 Sol in challenging evaluations of disclosure of broken search tools, explicit restrictions, and unauthorized outcomes during agentic tasks. The company observed no attempts to bypass an automated safety reviewer. These deliberately challenging tests do not measure typical-use failure rates.

## Pricing and availability

GPT‑6.1 Sol is available starting today to all Plus, Pro, Business, Enterprise, and Edu users in ChatGPT Work and Codex. It is not yet available in Chat. Developers can access it through the OpenAI API as `gpt-6.1-sol`.

Standard API prices are **$2 per million input tokens, $0.10 per million cached input tokens, and $10 per million output tokens**. OpenAI says that GPT‑6.1 Sol Ultrafast will be offered in the coming days with up to 8x faster token generation than standard speed in Codex.

OpenAI notes that its evaluations were performed in research environments or via the API and may differ from production ChatGPT because of system prompts, tools, efforts and related differences.
