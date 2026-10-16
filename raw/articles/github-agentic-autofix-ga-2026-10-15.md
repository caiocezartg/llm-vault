---
source_url: https://github.blog/changelog/2026-10-15-agentic-autofix-for-code-scanning-alerts-general-availability/
ingested: 2026-10-16
sha256: ac8c47c2870418a9133830b0d04a862a3b4cc3f8cf399a168609bcd242f4b004
---
# GitHub Code Security — Agentic Autofix GA (bounded primary capture)

Captured 2026-10-16 from GitHub’s 2026-10-15 changelog and supporting documentation.

GitHub made Agentic Autofix for code-scanning alerts generally available. A user assigns one or more default-branch alerts to Copilot; the agent explores relevant files, proposes a fix, reruns CodeQL, iterates as needed, and opens a draft PR containing its summary and validation steps. It supports assignment from a backlog/security campaign and via an alert API; GitHub documents batch selection of up to 25 alerts for one PR.

The feature needs enterprise/organization/repository policy enablement as applicable and consumes Code Security AI Credits plus GitHub Actions minutes. GitHub documents it as best effort: its validation reruns the standard CodeQL query suite and cannot confirm fixes for custom queries, the security-extended suite, or third-party-tool alerts. Generated changes still require review and tests before merge.

Primary URLs:
- https://github.blog/changelog/2026-10-15-agentic-autofix-for-code-scanning-alerts-general-availability/
- https://docs.github.com/enterprise-cloud@latest/code-security/concepts/code-scanning/autofix-for-code-scanning
