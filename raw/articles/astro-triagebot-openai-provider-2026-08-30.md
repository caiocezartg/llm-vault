---
source_url: https://github.com/withastro/triagebot-action/commit/51d30da13c0bd571a3822fc56882de40fead0086
ingested: 2026-08-30
sha256: 5b9e1a84f710f85ef1e243f9ee371776cf998cb9116e8ade3995e436ea4f8db1
---
## Primary source record

GitHub commit [`51d30da13c0bd571a3822fc56882de40fead0086`](https://github.com/withastro/triagebot-action/commit/51d30da13c0bd571a3822fc56882de40fead0086), authored and committed on 2026-08-28, adds `openai-api-key` as a supported credential to `withastro/triagebot-action`. The change allows `triage-model` and `verification-model` to use GPT model identifiers, alongside the existing Anthropic and Cloudflare Workers AI paths. The commit is verified by GitHub.

The action's workflow is stateful through GitHub issue labels. It runs separate reproduction, diagnosis, verification and fix stages, uses a skills directory for project-specific guidance, posts preview artifacts to the reporter, and can create a pull request after validation.

## Independent technical evidence

InfoQ's 2026-08-21 report described the production Astro deployment behind the action: its open issues fell from more than 200 to about 30. It emphasized the staged subagents, the `report.md` handoff instead of a shared execution context, preview releases for reporters, and human acceptance after validation. The report independently notes that the workflow became `triagebot-action` and that the wider Flue model persists execution history in an append-only event log.

Source URLs:
- Primary: https://github.com/withastro/triagebot-action/commit/51d30da13c0bd571a3822fc56882de40fead0086
- Independent evidence: https://www.infoq.com/news/2026/08/cloudflare-astro-ai-agents/
