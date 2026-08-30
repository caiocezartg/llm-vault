---
title: Hermes Agent
created: 2026-07-09
updated: 2026-08-24
type: entity
tags: [hermes, tool, agent, profile, skill, cron, memory, session-search]
sources: []
confidence: high
contested: false
contradictions: []
---

# Hermes Agent

Hermes Agent is the agent runtime used by Caio across Telegram, local tooling, profiles, skills, cron jobs, memory, session search, browser/web/file/terminal tools, and spawned profile workflows.

In this wiki, Hermes is treated as both:

1. a tool/runtime to be documented; and
2. the system whose profiles and agents use the wiki as external semantic context.

## Relevant concepts

- Profiles isolate configuration, memories, skills, sessions, and tool availability.
- Skills provide procedural knowledge.
- Memory stores compact durable facts.
- Cron jobs perform scheduled autonomous runs.
- Profile spawning allows one Hermes session to route work to another profile, such as `research` or `polaris`.

## Wiki-related profiles

- `polaris`: dedicated semantic archivist and LLM Wiki curator.
- `research`: dedicated research/deep-research profile; its [[projects/hermes-research-daily-radar]] uses Hermes-native discovery plus Agent Reach for broader candidate collection while keeping scoring and output limits authoritative.

## Desktop model-usage boundary

For compact Desktop usage panels, distinguish two different metrics instead of presenting them as one:

- **Focused-session context:** `host.state.focusedUsage` is reactive and follows the focused chat; it reports token/context consumption for that session.
- **Provider account quota:** reset windows and percentages are account/provider-level data, not model-context data. Reuse Hermes' backend account-usage adapters and expose only secret-free percentages, labels, plan metadata and reset times through a plugin-scoped REST route.

A thin Desktop connected to a remote Hermes backend has a split plugin boundary: install the JavaScript UI under the Desktop machine's actual `$HERMES_HOME/desktop-plugins/<id>/plugin.js`, and install/enable the Python backend under the remote runtime's `$HERMES_HOME/plugins/<id>/`. Desktop files hot-reload; newly enabled backend API routes require the remote Desktop backend to restart. This keeps credentials in the backend while the local renderer receives only display data.

For a compact usage surface that should behave like Hermes' built-in context indicator, contribute a declarative status-bar item with `variant: 'menu'` and `menuContent`, rather than a permanent pane or a custom-rendered trigger. The host then supplies the native upward-opening popover and status-bar interaction. Keep quota-window labels explicit (`Weekly`, `5hr`) rather than terse internal abbreviations (`wk`, `5h`). Account-level quota queries must be cached by their authority (`provider`/`model`), not by `focusedSessionId`; adding the session ID creates a new React Query identity and remote Desktop IPC/REST request on every chat switch even though the quota has not changed. Because `host.onEvent` fan-out is synchronous, listeners should also compare derived model/provider values and avoid cloning/publishing their session map for identical `session.info` payloads. This pattern complements the separation between semantic state and executable control in [[coding/architecture/project-memory-and-multi-model-handoff-layers]].

## Related

- [[concepts/global-llm-wiki]]
- [[decisions/use-polaris-for-global-llm-wiki]]
- [[projects/hermes-research-daily-radar]]
- [[comparisons/model-routing-hermes-opencode-pi]]
- [[concepts/model-context-protocol]] — MCP 2026-07-28 is the current future-integration baseline; the research profile's Agent Reach workflow remains intentionally non-MCP.
