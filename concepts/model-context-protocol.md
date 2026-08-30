---
title: Model Context Protocol
created: 2026-07-29
updated: 2026-08-13
type: concept
tags: [mcp, agent, workflow, api, research]
sources: [raw/articles/mcp-spec-2026-07-28.md, raw/articles/agent-plugins-spec-100-2026-08-13.md]
confidence: high
contested: false
contradictions: []
---

# Model Context Protocol (MCP)

MCP is an open protocol for connecting AI clients and agent runtimes to tools, resources and prompts. The `2026-07-28` release is a material protocol boundary: it replaces the stateful, bidirectional transport core with stateless request/response semantics. ^[raw/articles/mcp-spec-2026-07-28.md]

## 2026-07-28: migration-relevant changes

- `initialize`/`initialized` and `Mcp-Session-Id` are retired. Requests carry version, client identity and capabilities; `server/discover` is optional. Stateful applications should expose explicit handles rather than hide state in the transport. ^[raw/articles/mcp-spec-2026-07-28.md]
- `Mcp-Method` and `Mcp-Name` become mandatory headers for Streamable HTTP, enabling header-level routing, authorization and metering. List responses gain `ttlMs` and `cacheScope`. ^[raw/articles/mcp-spec-2026-07-28.md]
- MRTR replaces held-open server-to-client requests for interactivity. Tasks are formalized as an extension; DCR is deprecated in favor of CIMD; legacy HTTP+SSE, Roots, Sampling and Logging have at least a 12-month deprecation window. ^[raw/articles/mcp-spec-2026-07-28.md]

## Implications for Caio's workflows

**Interpretation:** the release makes remote MCP closer to an ordinary stateless HTTP workload, which reduces operational coupling for load balancing and makes policy enforcement at the gateway more practical. It does not by itself establish security or production readiness; explicit application handles, scoped authorization, isolated execution and independent acceptance gates remain necessary. See [[coding/architecture/merge-gated-dag-coding-workflow]] for the latter control-plane boundary.

The `research` profile's Agent Reach architecture deliberately does **not** use MCP. This protocol change is not a reason to install MCP servers or change that boundary. If a future project evaluates an MCP client/server, treat `2026-07-28` as the baseline and test: stateless retry behavior, header-based authorization/rate limits, explicit-handle lifecycle, MRTR approval paths, cache correctness and the old-transport migration. [[entities/tools/hermes-agent]] and [[projects/hermes-research-daily-radar]] provide the relevant Hermes context.

## Agent Plugins v1.0 packaging boundary

Agent Plugins `v1.0.0` packages two reusable component types around agent clients: Agent Skills and MCP server configurations. It is a directory format centered on `plugin.json`, optional `skills/`, and optional root `mcp.json`; it does not replace MCP's transport or authorization semantics. Package-relative paths are required to stay under the resolved plugin root, but that check does **not** sandbox plugin subprocesses or limit runtime input paths. ^[raw/articles/agent-plugins-spec-100-2026-08-13.md]

For Caio's cross-harness workflows, treat the format as optional portability plumbing: provenance/pinning, client-by-client compatibility, MCP allowlists, egress policy, scoped credentials, isolated execution and independent repository gates remain external controls. The research profile remains intentionally non-MCP for Agent Reach. See [[comparisons/model-routing-hermes-opencode-pi]] for the broader skills/distribution boundary and [[entities/tools/hermes-agent]] for runtime context.

## Evidence and review trigger

The official specification announced Tier-1 SDK support in TypeScript, Python, Go and C#. An independent Hacker News submission had 115 points and 37 comments when checked on 2026-07-29; this supports immediate developer attention, not a claim of broad production adoption.

Revisit this page when a Hermes-supported MCP integration or a system Caio operates moves to the new revision, or when compatibility experience contradicts the stated migration path.

## Sources

- [MCP 2026-07-28 announcement](https://blog.modelcontextprotocol.io/posts/2026-07-28/)
- [Hacker News discussion](https://news.ycombinator.com/item?id=49088058)
