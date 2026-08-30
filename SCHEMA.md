# LLM Wiki Schema

## Domain

This is Caio's global Hermes knowledge base: a cross-profile, Obsidian-compatible LLM Wiki for durable knowledge used by research, coding, architecture, agent orchestration, model/tool evaluation, debugging, decisions, and reusable workflows.

It is not limited to the `research` profile. It is intended to be useful to `default`, `research`, `polaris`, future coding profiles, cron jobs, and spawned agents.

## Purpose

Polaris and other Hermes profiles use this wiki as an external semantic memory layer:

- a glossary for recurring concepts;
- a catalog of tools, models, frameworks, companies, projects, and systems;
- a record of durable technical decisions;
- a library of coding/debugging/architecture patterns;
- a place for reusable research syntheses and comparisons;
- an Obsidian vault for human navigation and manual editing.

## Directory Structure

```text
llm-wiki/
├── SCHEMA.md
├── index.md
├── log.md
├── raw/
│   ├── articles/
│   ├── papers/
│   ├── transcripts/
│   ├── docs/
│   └── assets/
├── entities/
│   ├── models/
│   ├── tools/
│   ├── companies/
│   ├── frameworks/
│   └── projects/
├── concepts/
├── comparisons/
├── decisions/
├── coding/
│   ├── patterns/
│   ├── debugging/
│   ├── architecture/
│   └── runbooks/
├── projects/
└── queries/
```

## Operating Rules

- Always orient first: read `SCHEMA.md`, `index.md`, and recent `log.md` before wiki operations.
- Use lowercase kebab-case filenames: `agent-orchestration.md`, `ollama-cloud-agent-models.md`.
- Every wiki page starts with YAML frontmatter.
- Use `[[wikilinks]]` to connect related pages.
- Prefer updating existing pages over creating duplicates.
- Every new page must be added to `index.md`.
- Every wiki-changing operation must be logged in `log.md`.
- Raw sources in `raw/` are immutable; do not rewrite them except to correct ingestion metadata immediately after creation.
- For synthesized claims from multiple sources, add provenance markers like `^[raw/articles/source.md]` when useful.
- Ask before mass-updating 10+ existing pages or changing this schema substantially.

## Frontmatter

```yaml
---
title: Page Title
created: YYYY-MM-DD
updated: YYYY-MM-DD
type: entity | concept | comparison | decision | coding-pattern | debugging-note | architecture | runbook | project | query | summary
tags: [from taxonomy below]
sources: []
confidence: high | medium | low
contested: false
contradictions: []
---
```

`confidence`, `contested`, and `contradictions` are especially important for fast-moving AI/model/tool claims.

## Raw Source Frontmatter

```yaml
---
source_url: https://example.com/source
ingested: YYYY-MM-DD
sha256: <hex digest of body after frontmatter>
---
```

## Tag Taxonomy

Use these tags first. Add new tags here before using them.

### AI / LLMs
- llm
- model
- benchmark
- evaluation
- inference
- context-window
- tool-calling
- function-calling
- reasoning
- multimodal
- open-weight

### Agents / Automation
- agent
- agent-orchestration
- multi-agent
- workflow
- cron
- mcp
- browser-automation
- computer-use
- agent-reach

### Hermes / Tooling
- hermes
- profile
- skill
- memory
- session-search
- obsidian
- llm-wiki
- ollama
- openrouter

### Software Development
- coding
- debugging
- architecture
- testing
- devops
- api
- cli
- python
- javascript
- repository

### Knowledge Management
- decision
- comparison
- glossary
- runbook
- research
- source
- contradiction
- convention

### Entities
- company
- tool
- framework
- project
- person

## Page Thresholds

Create or update a page when:

- an entity/concept appears in 2+ durable contexts;
- it is central to one important source or decision;
- it captures a reusable workflow, coding pattern, or architecture decision;
- it is a comparison likely to be useful again;
- it defines a convention that future agents should follow.

Do not create pages for:

- one-off task progress;
- temporary TODOs;
- stale artifact IDs, commits, issue numbers, or PR numbers unless part of a durable architecture/decision page;
- passing mentions;
- content better stored as a Hermes memory or skill.

## Page Types

### Concepts
Definitions and explanations of recurring ideas: agent orchestration, MCP, context engineering, tool calling, deep research.

### Entities
Models, tools, companies, frameworks, projects, and people.

### Comparisons
Side-by-side analyses with a clear comparison axis and source references.

### Decisions
Durable decisions: what was chosen, why, alternatives considered, date, confidence, review trigger.

### Coding
Patterns, debugging notes, architecture notes, and runbooks that help future coding tasks.

### Queries
Filed answers worth keeping because they would be expensive to re-derive.

## Update Policy

When new information conflicts with existing content:

1. Check source dates and authority.
2. Prefer newer primary sources where appropriate.
3. If unresolved, keep both claims with dates and sources.
4. Mark `contested: true` and add `contradictions` where relevant.
5. Surface the contradiction in the user-facing report or lint output.

## Obsidian Conventions

- `[[wikilinks]]` are preferred for internal links.
- Attachments belong in `raw/assets/`.
- Dataview-friendly frontmatter is required on all non-raw wiki pages.
- The vault should remain readable as plain Markdown without Obsidian.
