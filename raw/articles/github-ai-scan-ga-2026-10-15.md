---
source_url: https://github.blog/changelog/2026-10-15-ai-scan-for-pull-requests-generally-available/
ingested: 2026-10-16
sha256: e3e9f0da58c240b09b39c16b2081e65c59983b56f9e76a0fab166fd3616d6a5d
---
# GitHub Code Security — AI Scan for pull requests GA (bounded primary capture)

Captured 2026-10-16 from GitHub’s 2026-10-15 changelog and supporting documentation.

GitHub made Code scanning AI Scan for pull requests generally available. It complements CodeQL by analyzing pull-request changes in languages/frameworks CodeQL does not currently cover, including PHP, Shell/Bash, Terraform HCL, Dockerfiles, JSP and Blazor. It runs automatically when code scanning and the effective repository setting are enabled; results are labeled “AI” beside CodeQL findings.

The documented enforcement boundary is explicit: findings are advisory, do not fail the code-scanning check, and cannot satisfy ruleset merge requirements. It does not scan fork or Dependabot PRs, performs no full-repository scan, can return false positives, and may use repository code search. AI Scan is billed through Code Security AI Credits; organization-level enablement can begin consumption across eligible repositories before individual repository opt-out.

Primary URLs:
- https://github.blog/changelog/2026-10-15-ai-scan-for-pull-requests-generally-available/
- https://docs.github.com/enterprise-cloud@latest/code-security/concepts/code-scanning/ai-powered-security-detections
