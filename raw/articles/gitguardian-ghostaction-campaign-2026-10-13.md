---
source_url: https://blog.gitguardian.com/ghostaction-github-actions-supply-chain-attack-returns/
ingested: 2026-10-14
sha256: 0352397a9b52d52b52ed7c0135de37d6a93a20dc1d4468a88cfe94e96f58ddd5
---
# GitGuardian / Socket — GhostAction campaign escalation

- Primary investigation: https://blog.gitguardian.com/ghostaction-github-actions-supply-chain-attack-returns/
- Independent technical investigation: https://socket.dev/blog/ghostaction-cloud-credentials
- Latest primary update: 2026-10-13

## Bounded source record

GitGuardian’s 13 October update reports an accelerated GhostAction campaign from 8–12 October: more than 30,000 repositories across 3,000 users/organizations were targeted after compromise of about 1,900 GitHub users. Its dataset records attempted extraction of 3,174 secrets from public-repository CI. GitGuardian reports that GitHub began preventing the malicious workflow from running on 9 October, so later waves observed on 10 and 12 October could not extract secrets; the update does not establish that every targeted repository had a successful run.

The malicious workflows masquerade as security audits, run on push, use `actions/checkout` with full history in variants, collect GitHub Actions secrets plus credential-like material from the working tree and Git history, then POST to an attacker-controlled endpoint. GitGuardian’s earlier 2026 scope was 772 public repositories, 373 users/organizations and 2,577 targeted secret names from 31 August to 30 September; the October figures are a newer, broader update and should not be combined as a single victim total.

Socket independently documented an 8 October burst that used compromised maintainer accounts to add `security-audit.yml` to 346 repositories, including organization-owned repositories. It observed successful workflow runs and a broadened scan for cloud and AI-service credentials in repository contents and full Git history. Its report establishes a concrete delivery mechanism and indicators, while its wider account/repository counts are investigator observations rather than a GitHub incident report.

## Durable implication

A protected integration boundary must treat workflow-definition changes as privileged code: a maintainer-account compromise that can push to a default branch can introduce an Actions workflow able to consume that repository’s CI secrets. Keep direct pushes to protected branches off for sensitive repositories; require review/status gates for `.github/workflows/**`; scope and rotate CI credentials; maintain egress/audit telemetry; and rehearse incident response that revokes compromised account credentials and investigates source history, Actions runs and downstream package releases. Secret scanning/push protection and GitHub-side blocking reduce exposure but are not substitutes for branch protection, least privilege, provenance review and recovery controls.
