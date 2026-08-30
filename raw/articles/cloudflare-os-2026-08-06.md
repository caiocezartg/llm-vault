---
source_url: https://blog.cloudflare.com/cloudflare-os/
ingested: 2026-08-06
sha256: cf0fa3de2b005a4bf2a52280535741c17b246e8d6ef4b3c69b159f12e99bb36a
---

# Cloudflare OS — primary-source excerpt (2026-08-06)

Cloudflare announced and open-sourced Cloudflare OS on 2026-08-05. The project is an Apache-2.0 agent workspace built on Cloudflare Workers for creating documents and apps and for running agents over an organization’s context and connected systems.

The announced architecture combines: (1) a browser-facing agent workspace with persistent state, files, outputs and an isolated code-execution runtime; (2) a security and governance layer for internal services and data; and (3) a platform for personal, modifiable apps. Cloudflare says it had deployed an earlier version internally in May, with thousands of staff using it daily, and rebuilt the public version after finding that ordinary MCP/tool permissions did not answer which resources an agent had observed when outputs or workspaces were shared.

The durable design claim worth evaluating is authorization inheritance: an agent should not grant a collaborator more access than that collaborator already holds. The announcement is not independent proof that isolation, connector policy, or indirect-prompt-injection resistance are complete. Cloudflare’s own deployment and public repository establish availability and intended architecture; production suitability still requires a scoped, adversarial test in the adopter’s tenancy.

Primary sources:
- https://blog.cloudflare.com/cloudflare-os/
- https://blog.cloudflare.com/how-we-use-ai-with-cloudflare-os/
- https://github.com/cloudflare/cloudflare-os
