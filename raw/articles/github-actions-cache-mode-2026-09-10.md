---
source_url: https://github.blog/changelog/2026-09-10-control-github-actions-cache-access-with-cache-mode
ingested: 2026-09-11
sha256: e70a4fe405e379749b9a791ab118f49f49c48477c463ea293575ffe141f78fe8
---
# GitHub Actions cache-mode — bounded primary capture

GitHub made `cache-mode` generally available on 2026-09-10 for all plans. Workflow or job policies can be `read`, `write`, `write-only`, or `none`; the cache service enforces the selected level and a reusable called workflow cannot receive more access than its caller grants.

Explicit read access for low-trust pull request jobs and isolated write-only cache seeders make cache authority reviewable. An explicit write or write-only setting on low-trust events can still increase cache-poisoning risk, so GitHub emits a warning; the annotation is not an enforcement substitute.

Independent security discussion documents cache poisoning as a relevant CI/CD risk and the migration guide calls out the performance consequence that denied access can degrade to a cache miss rather than failing the job.

Sources:
- https://github.blog/changelog/2026-09-10-control-github-actions-cache-access-with-cache-mode
- https://github.com/orgs/community/discussions/194493
- https://axentia.in/blog/github-actions-cache-mode-ci-migration