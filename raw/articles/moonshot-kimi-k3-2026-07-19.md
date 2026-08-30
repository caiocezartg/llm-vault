---
source_url: https://www.kimi.com/blog/kimi-k3
ingested: 2026-07-19
sha256: a6fcda6385da7bbe16913bfc2efff6ecfcee53fed2a82dca0f6a974e600abbbb
---
# Kimi K3 — primary-source capture

Moonshot AI's 16–17 July 2026 Kimi K3 announcement describes a 2.8-trillion-parameter Mixture-of-Experts model with native vision and a stated one-million-token context window. The company says K3 is available through Kimi.com, Kimi Work, Kimi Code, and the Kimi API; full weights and a technical report are planned by 27 July 2026.

The API documentation identifies the model name as `kimi-k3`, exposes OpenAI-SDK-compatible Chat Completions, reasoning output, strict JSON Schema output, function/tool calling, automatic context caching, and a maximum `max_completion_tokens` value of 1,048,576. It warns that multi-turn and tool workflows must return the complete assistant message, not just final content.

Material operational limitations stated by Moonshot: only `reasoning_effort=max` is currently supported; the company says quality can be unstable if the harness does not preserve full thinking history or if a session switches from another model mid-run; the model can make unexpectedly proactive decisions under ambiguous intent; claimed benchmark results mix KimiCode/Claude Code/Codex harnesses and include first-party evaluation.

Source URLs:
- https://www.kimi.com/blog/kimi-k3
- https://platform.kimi.ai/docs/guide/kimi-k3-quickstart
