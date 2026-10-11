---
source_url: https://www.cockroachlabs.com/blog/experiment-running-hospital-code/
ingested: 2026-10-11
sha256: ec6a8c56832bf24b4340c88b322825cdc14d12b4430ee7c6ea9fca5fdf38ada1
---
# Cockroach Labs — Five months treating bugs like patients and coding agents like a medical team

Primary-source excerpt captured for durable workflow analysis.

Cockroach Labs reported on 9 October 2026 that it had run its “MOLT Sinai” agentic coding pipeline for just under five months against its database-migration tooling. The company says the pipeline merged more than one million lines of code in changes small enough for review, and that it used GitHub Actions with issue labels plus scratch files as workflow state.

For its IBM Db2 migration-support example, the company reports that an initial issue was decomposed into 15 dependent sub-issues, later expanding to 32 issues, 27 merged pull requests, 55 review returns, and nine escalations (two to a human). It says the work completed in under two days at a reported token cost of US$4,172, compared with a 2024 Oracle-support project that took nine months and about US$160,000 in engineering time. These are first-party, non-comparable claims rather than an independently audited productivity result.

The stated control plane uses distinct agent roles: a Triage Nurse classifies/admit-rejects work; a Fellow performs investigation, planning and implementation; a separate Review Attending approves or rejects the plan and code; a Discharge Nurse verifies that process conditions were met; and a human Chief of Medicine handles unresolved cases. The company also describes a periodic “Charge Nurse” for stalled work, an “Infection Control” stop mechanism when main breaks, and recurring process reviews.

The write-up is most explicit about its operational limitation: after one initial autonomous week, Cockroach Labs enabled human-approval mode, requiring every merge to receive human review. The team says that it is still confirming the correctness of the initial Db2 experiment, whose code was not reviewed during the first test. The reported system therefore supports a thesis about staged planning, independent review and explicit escalation; it does not establish that a fully autonomous multi-agent pipeline is production-safe.

Source: https://www.cockroachlabs.com/blog/experiment-running-hospital-code/
Published: 2026-10-09
Captured: 2026-10-11
