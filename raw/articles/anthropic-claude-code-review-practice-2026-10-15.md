---
source_url: https://claude.dev/blog/solving-code-review-at-anthropic/
ingested: 2026-10-17
sha256: 9d881595ff2453bf28cf282960d76120955a972be5aa3a66d1d893cef3a21ae5
---

# Bounded source capture — Anthropic: Claude Code review practice

Source published 2026-10-15. Anthropic reports that, from June to September, merged pull requests in the Claude Code codebase more than doubled while the share reverted fell by more than 40%. These are internal operational figures, not a controlled causal benchmark.

The described control pattern is layered: executable pre-PR verification plus a fresh-context agent review; required CI; parallel AI bug-finding with separate agent verification; a security pass that can block; risk-based human approval; merge-queue revalidation; staged release/flags; and fast rollback.

The team measures human approvals, human comments and time waiting on people, but treats reverts and incidents as the guardrail. Human approval tiers are set by change risk, not author identity; sensitive paths (including CI workflow files) retain mandatory human review, and an agent approval cannot fill a human-approval requirement.

To control review loops, Anthropic reports capping rounds, rerunning only new diffs after early passes, preventing repeat findings, and turning incidents/reverts into a daily regression evaluation set. The article still acknowledges open risks around loss of shared codebase understanding and the need for circuit breakers before broader zero-human merges.

This is an immutable bounded capture of the primary article; see the source URL for the complete source.
