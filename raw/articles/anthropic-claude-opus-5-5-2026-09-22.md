---
source_url: https://www.anthropic.com/claude-opus-5-5
ingested: 2026-09-23
sha256: d22bb4e5b9ec05e14943521b55ada4309d1b11f07d09b8115b113e2bef493996
---
# Introducing Claude Opus 5.5

Source URL: https://www.anthropic.com/claude-opus-5-5
Retrieved: 2026-09-23

Anthropic announced Claude Opus 5.5 on 2026-09-22 as the first model in its 5.5 family. It is available as `claude-opus-5-5`, with a 1M-token context window, US$4/M input tokens, US$20/M output tokens and US$0.20/M cache reads. The vendor says it is faster and cheaper than Claude Opus 5 and reports strong results in coding and computer-use evaluations; those launch comparisons are configuration-specific vendor evidence.

The announcement says Opus 5.5 uses adaptive thinking and has external pre-release evaluations including METR and Frontier Design. It also documents safety fallbacks and availability across Anthropic, AWS, Google Cloud and Azure routes. The API release notes specify integration incompatibilities: thinking cannot be disabled, `tool_choice` values `any` and named `tool` return HTTP 400, and computer use needs the current toolset on Anthropic API and Google Cloud.

Claude Code v2.1.280 makes Opus 5.5 the default Opus model and fixes a symlink-path authorization issue: policy evaluation now uses the location where a write lands rather than an in-tree spelling. It also improves auto-mode retry handling and emits hook output size information through OpenTelemetry.
