---
source_url: https://blog.cloudflare.com/next-git-platform-on-cloudflare/
ingested: 2026-10-04
sha256: e36acd46215a0c119f6e091b64d23ca81bfd074f0b680eeac04ee9b89d1275e2
---
# Cloudflare Artifacts open-beta expansion — bounded primary-source record

**Source title:** We want you to build the next Git platform on Cloudflare  
**Captured:** 2026-10-04

Cloudflare describes Artifacts as a versioned filesystem that speaks Git. In the current announcement it says Artifacts is in open beta and can programmatically create and fork repositories, keep versioned code and agent context, and expose Git operations to workflows. It adds integration with Workers Builds: pushes to a production branch can deploy a Worker, while pushes to other branches can create or update Workers Previews.

The announcement documents a Workers binding that can create or fork repositories, inspect files and commits, issue repository-scoped Git tokens, and read task instructions such as `AGENTS.md`. It also documents events for repository creation, import, fork, deletion, push, clone and fetch; these can trigger CI or a review workflow. Namespace-level U.S. or EU data-jurisdiction choices and repository operation/error metrics are available. Cloudflare says billing begins on 2026-10-15.

The article positions these primitives as components for agent coordination, but does not establish that any workflow is safe or correct by default. Its examples are vendor architecture, not evidence that an agent should receive production credentials, deploy authority, or acceptance authority without external controls.

Primary URLs:
- https://blog.cloudflare.com/next-git-platform-on-cloudflare/
- https://developers.cloudflare.com/artifacts/
- https://www.cloudflare.com/git-competition/
