---
title: Hermes Research Daily Radar
created: 2026-07-14
updated: 2026-07-14
type: project
tags: [project, hermes, profile, research, workflow, agent-reach, cli, api]
sources:
  - /home/caiocezartg/research-workflow/README.md
  - /home/caiocezartg/research-workflow/topics.yaml
  - /home/caiocezartg/research-workflow/prompts/daily-research-radar.md
  - /home/caiocezartg/.hermes/profiles/research/skills/agent-reach/SKILL.md
confidence: high
contested: false
contradictions: []
---

# Hermes Research Daily Radar

The `research` profile's Daily Research Radar is a selective Hermes cron workflow for software-development and AI-engineering discovery. Its architecture is hybrid: Hermes-native web/search/extraction, wiki orientation, cron, skills and persisted reports remain the control plane, while Agent Reach v1.5.0 is used as a read-only candidate-expansion layer.

## Durable architecture decision

Agent Reach is installed in an isolated user venv at `~/.agent-reach-venv`, with commands exposed through `~/.local/bin`. The local `agent-reach` skill requires `agent-reach doctor --json` before broad discovery and forbids treating installed-but-unauthenticated CLIs as evidence of platform coverage.

Zero-config channels validated for this workflow are GitHub public discovery via REST/web, YouTube via `yt-dlp`, V2EX public API, RSS/Atom via `feedparser`, web-page fallback through Jina Reader, and Bilibili via `bili-cli`. The CLIs `gh`, `twitter-cli`, and `rdt-cli` are installed but remain authentication-pending; they are not used unless doctor/auth status confirms they are usable.

The workflow explicitly does not use MCP, `mcporter`, Exa MCP, OpenCLI, browser-session backends, or new MCP servers. This keeps the radar VPS-friendly and aligned with the Hermes-native tool surface.

## Selection invariant

Agent Reach can increase the candidate pool, but it does not increase output volume or weaken selection. Scoring, hard gates, deduplication, final item limits, and the rule to prefer silence over filler remain governed by `topics.yaml` and the radar prompt.

## Related

- [[entities/tools/hermes-agent]]
- [[concepts/global-llm-wiki]]
- [[coding/architecture/kitdev-deterministic-agentic-workflows]]
