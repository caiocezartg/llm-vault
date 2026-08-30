---
title: Global LLM Wiki
created: 2026-07-09
updated: 2026-07-20
type: concept
tags: [llm-wiki, obsidian, hermes, glossary, research, coding]
sources:
  - https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
  - /home/caiocezartg/reports/llm-wiki-usage-patterns-2026-07-19.md
confidence: high
contested: false
contradictions: []
---

# Global LLM Wiki

The Global LLM Wiki is Caio's cross-profile knowledge layer for Hermes. It is an Obsidian-compatible Markdown vault used to preserve durable knowledge across research, coding, architecture, model/tool evaluation, debugging, decisions, and reusable workflows.

It is maintained primarily by [[decisions/use-polaris-for-global-llm-wiki|Polaris]], but it is intended to be useful to all Hermes profiles, including research and future coding profiles.

## Purpose

The wiki exists to prevent recurring knowledge from being trapped in transient chat sessions. It stores:

- durable concepts and glossary entries;
- tool/model/framework/entity notes;
- coding and debugging patterns;
- architecture notes and runbooks;
- reusable research syntheses;
- comparisons and technical decisions.

## Relationship to Hermes memory and skills

- Hermes **memory** stores compact user preferences and stable personal/environment facts.
- Hermes **skills** store reusable procedures.
- The **LLM Wiki** stores dense, structured, interlinked knowledge.
- Session history stores what happened in previous conversations.

## Usage pattern

Before tasks involving recurring concepts, prior decisions, known tools/models/projects, coding conventions, or reusable research, agents should consult `index.md`, search the vault, and read relevant pages.

After substantial work, agents should update the wiki only when the result is durable and likely to help future tasks.

## Observed public usage patterns (2026-07)

A review of nine public projects/implementations plus the original Karpathy gist found no single normative product or directory tree. The recurring faithful shape is a Markdown-first separation between preserved sources (`raw/`, `sources/`, or archived `inbox/`), synthesized wiki pages, agent-readable schema/instructions, `index.md`, `log.md`, and structural lint. Obsidian, graph views, BM25/vector search, MCP, databases, review queues, and collaborative services are optional extensions rather than defining requirements.

Public examples visibly target personal/global research, topic/domain wikis, project-local workspaces for coding agents, and a smaller number of team/multi-agent memory systems. Project-local layouts are recurrent among published coding-agent skills, but the public sample does not establish mature per-repository wikis as an industry-wide convention. Monorepo and product-level multi-repo layouts are defensible adaptations, not prevalence claims.

For software, keep authority split explicitly: code/tests own executable behavior; README owns public entry points; `AGENTS.md`/`CLAUDE.md` own agent operating instructions; ADRs own approved architectural decisions; specs own current change intent; issue trackers own mutable work state; handoffs own immediate continuation; and the wiki owns durable synthesis, relationships, glossary, validated debugging knowledge, and navigation. Promote only reusable local findings to the global wiki.

Practical rollout: begin with Markdown, links, schema/index/log and deterministic lint; add search, graph, CI, automated promotion, or multi-agent coordination only after measured retrieval or maintenance problems. See the full sourced report at `/home/caiocezartg/reports/llm-wiki-usage-patterns-2026-07-19.md`.

## Related

- [[entities/tools/hermes-agent]]
- [[decisions/use-polaris-for-global-llm-wiki]]
