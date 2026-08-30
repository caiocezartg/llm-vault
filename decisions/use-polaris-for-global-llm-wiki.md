---
title: Use Polaris for Global LLM Wiki
created: 2026-07-09
updated: 2026-07-09
type: decision
tags: [decision, llm-wiki, obsidian, hermes, profile]
sources: []
confidence: high
contested: false
contradictions: []
---

# Use Polaris for Global LLM Wiki

## Decision

Create a dedicated Hermes profile named `polaris` to maintain Caio's global LLM Wiki / Obsidian vault.

## Rationale

Polaris is a star-name profile that acts as a north star for durable knowledge: a stable point of orientation for other Hermes profiles and tasks.

The wiki should not be tied only to the `research` profile. It should be a general-purpose semantic memory layer that can support:

- research and deep research;
- coding tasks;
- architecture decisions;
- model/tool comparisons;
- debugging patterns;
- reusable workflows;
- future Agent Reach integration.

## Implementation

- Profile: `polaris`
- Vault path: `/home/caiocezartg/llm-wiki`
- Environment variables:
  - `WIKI_PATH=/home/caiocezartg/llm-wiki`
  - `OBSIDIAN_VAULT_PATH=/home/caiocezartg/llm-wiki`

## Related

- [[concepts/global-llm-wiki]]
- [[entities/tools/hermes-agent]]
