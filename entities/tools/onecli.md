---
title: OneCLI
created: 2026-07-24
updated: 2026-08-20
type: entity
tags: [tool, agent, workflow, api, devops, cli]
sources:
  - https://github.com/onecli/onecli
  - https://github.com/onecli/onecli/commit/1633c21e20874f7d9add80f2d566c7c5424070d4
  - https://news.ycombinator.com/item?id=49023427
  - raw/articles/onecli-v2-2026-08-20.md
confidence: medium
contested: false
contradictions: []
---

# OneCLI

## Overview

OneCLI is an Apache-2.0 credential gateway for AI agents. It accepts proxied HTTP requests, matches policy by destination and request shape, injects credentials outside the agent process, and forwards permitted calls. The intended boundary is that agents use placeholders rather than obtain the real API keys. Its public implementation combines a Rust gateway with a Next.js dashboard and a PostgreSQL-backed configuration surface. [Repository](https://github.com/onecli/onecli)

The durable pattern is more important than this implementation: keep the secret store and authorization decision outside an agent's filesystem, prompt context, tool transcript, and code-generation environment. This aligns with the containment guidance in [[entities/models/gpt-5-6]] and is complementary to the role separation and independent validation patterns in [[entities/tools/cloudflare-security-audit-skill]].

## Material security update — 2026-07-23

A public commit fixed a mismatch in which credential injection could cover a host that policy enforcement did not cover. The stated bypass involved an agent switching from a policy-covered endpoint to an alternate host where the credential was still injected; the fix derives enforcement coverage from the injection surface and adds an `enforcement ⊇ injection` invariant. The code change and its tests are useful evidence of active maintenance, but they also demonstrate why an unreviewed credential gateway must not be treated as a security guarantee. [Fix commit](https://github.com/onecli/onecli/commit/1633c21e20874f7d9add80f2d566c7c5424070d4)

For any proxy-enforced agent policy, test the full credential surface—not only the canonical API hostname. Include alternate and regional hosts, path aliases, redirects, methods, raw-content/CDN endpoints, and failure behavior. The desired property is fail-closed enforcement that is at least as broad as credential injection.

## v2.0: workspaces, split services and hosted agents — 2026-08-18

OneCLI `v2.0.0` introduces workspaces, split services and hosted agents; `v2.0.1` then fixes chat-native approval cards, cross-surface synchronization and channel seams. The public release is a material expansion from credential gateway toward a team-agent workspace, but its terse notes do not verify isolation, request binding, authorization correctness or production reliability. ^[raw/articles/onecli-v2-2026-08-20.md]

The Launch HN discussion gave this change a useful adversarial signal: participants asked whether approvals bind to exact method, URL and body; whether policy can restrict paths, request fields, resource ownership and response volume; and how it differs from competing harnesses. The authors state policy matches method, path and body on a host, but that remains a first-party description. A trial must exercise adversarial request shapes, alternate hosts, redirects, approval expiry, gateway failure and audit receipts before treating v2 as a secure control plane. [[coding/architecture/merge-gated-dag-coding-workflow]] remains the delivery authority.

## Boundary and limitations

A gateway can prevent direct disclosure of a secret to an agent and reject disallowed requests at the network layer. It does **not** make an agent harmless once an allowed operation is reachable: an injected credential can still authorize destructive calls within its policy; egress, sandboxing, service-side scopes, short-lived credentials, audit logging, budget/rate limits, and human approval for sensitive operations remain necessary. This is a control-plane component, not a replacement for the sandbox and evaluation-containment controls recorded in [[coding/architecture/kitdev-deterministic-agentic-workflows]].

## Controlled trial guidance

Use a synthetic project and non-production credentials. Put the gateway outside the agent sandbox, deny direct egress, and define an explicit matrix of `credential × host × path × method × policy decision`. Verify that alternate routes cannot bypass block/approval rules, that approvals fail closed on gateway errors, and that logs do not retain secrets. Compare the operational burden against provider-native short-lived, narrowly scoped credentials before introducing a persistent gateway.

## Evidence and caveats

At the 24 July 2026 collection, the repository displayed 2.7k stars, 155 forks, 304 commits, and a recent public fix; its latest published release page was `v1.41.0` from 7 July. A same-day Show HN had 83 points and 29 comments, with practical questions about OAuth, browser cookies, retry behavior, competing credential brokers, and the trust boundary. Those are attention and design-review signals, not an independent security audit or proof of production safety. [HN discussion](https://news.ycombinator.com/item?id=49023427)

## Sources

- [OneCLI repository, implementation, license, and release history](https://github.com/onecli/onecli)
- [Host-enforcement bypass fix](https://github.com/onecli/onecli/commit/1633c21e20874f7d9add80f2d566c7c5424070d4)
- [Release v1.41.0](https://github.com/onecli/onecli/releases/tag/v1.41.0)
- [Show HN discussion](https://news.ycombinator.com/item?id=49023427)

## Related

- [[entities/models/gpt-5-6]]
- [[entities/tools/cloudflare-security-audit-skill]]
- [[coding/architecture/kitdev-deterministic-agentic-workflows]]
- [[entities/tools/hermes-agent]]
