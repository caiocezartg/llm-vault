---
title: npm stage-only tokens
created: 2026-09-19
updated: 2026-09-19
type: concept
tags: [testing, devops, workflow, api, convention]
sources: [raw/articles/npm-stage-only-tokens-2026-09-18.md]
confidence: medium
contested: false
contradictions: []
---

# npm stage-only tokens

## What changed

npm granular access tokens can now be restricted to **stage only**: CI can upload a release candidate with `npm stage publish`, but the registry rejects a direct `npm publish`. A maintainer must inspect and promote the stage with 2FA before it becomes installable. npm states that direct publishing through bypass-2FA granular tokens will be removed in January 2027. ^[raw/articles/npm-stage-only-tokens-2026-09-18.md]

## Engineering boundary

This is a narrowly useful capability split: a CI credential can prepare a version but cannot make a new version live. It does **not** make the credential harmless: it retains dist-tag and deprecation powers, and does not substitute for scoped packages, OIDC/trusted publishing, protected CI, provenance checks, review of the staged tarball, or incident controls. ^[raw/articles/npm-stage-only-tokens-2026-09-18.md]

## Adoption pattern

For token-based npm publishing that cannot yet use OIDC, replace direct publishing with a scoped stage-only token; pin npm CLI 11.15+ and Node 22.14+; use `npm stage view` or download before approval; and make the approving maintainer/2FA step a named release gate. Test a rejected direct-publish attempt and an approved staged release in a disposable package before changing production release automation. [[concepts/github-actions-cache-capability-modes]] and [[coding/architecture/merge-gated-dag-coding-workflow]] provide compatible patterns: explicit capability allocation, trusted promotion paths, and external acceptance evidence.

## Evidence status

The registry behavior and 2027 migration date come from npm/GitHub documentation. InfoQ and the Hacker News discussion independently describe both the CI-takeover reduction and operational friction for monorepos; neither demonstrates adoption rates or proves that staging blocks all supply-chain compromise paths. ^[raw/articles/npm-stage-only-tokens-2026-09-18.md]
