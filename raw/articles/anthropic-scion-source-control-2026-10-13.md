---
source_url: https://www.anthropic.com/engineering/redesigning-source-control
ingested: 2026-10-15
sha256: c629c5cfab5fe0764aa432dac1d25e1db8b713feea2a1f91f0c4767f73b008bc
---
# Anthropic: Redesigning source control at Anthropic — bounded primary capture

Published: 2026-10-13

Anthropic reports that its code changes merged per day rose from about 2,500 in May 2026 to more than 30,000 in September. It states that the main-branch history of its monorepo is almost 100 GB, a compressed working copy exceeds 25 GB, and CI alone performs roughly 25 million checkouts per day.

The company built and migrated to an internal source-control system, Scion, in five months. Scion is designed for always-online clients such as agents and jobs: server-side services perform history/blame queries, commit/rebase/merge operations and expose source-control queries by API. Clients keep bounded local caches; sparse and virtualized checkouts aim to materialize only required data. Anthropic says Git remains the right design for the vast majority of repositories and that Scion is not a broadly deployable product because it requires bespoke source control, code review, code search and CI.

Reusable interpretation: agent-induced code volume shifts some bottlenecks from generation to checkout, source-control queries, merge/review capacity and CI. This is an architecture case study, not a general recommendation to replace Git or a demonstrated quality/throughput multiplier for other teams. Preserve independent review, SHA-bound gates and post-merge observation as agent concurrency increases.

Primary URL: https://www.anthropic.com/engineering/redesigning-source-control
Independent discussion signal: https://news.ycombinator.com/item?id=50073633
