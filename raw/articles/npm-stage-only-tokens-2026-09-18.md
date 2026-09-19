---
source_url: https://github.blog/changelog/2026-09-18-stage-only-npm-tokens-for-safer-automation/
ingested: 2026-09-19
sha256: a5ec97b7b063530cc28f58aaf20a086e62b3849d32274e0563faa0a91bede0e8
---
# GitHub/npm: stage-only tokens for safer automation

Source URL: https://github.blog/changelog/2026-09-18-stage-only-npm-tokens-for-safer-automation/
Retrieved: 2026-09-19

GitHub announced that npm granular access tokens can now use `Read and write (stage only)`. A workflow using such a token must submit a version with `npm stage publish`; direct `npm publish` is rejected. A maintainer then reviews and promotes the stage with 2FA before it becomes installable.

The source states that the token still retains other write permissions, including moving dist-tags and deprecating versions, so it is not a general security boundary. The feature is opt-in, requires npm CLI 11.15.0+ and Node.js 22.14.0+ for staged publishing, and provides a migration route before npm removes direct publishing through bypass-2FA tokens in January 2027.

Independent context: InfoQ's 2026-08-07 report describes staged publishing as an explicit human-approval step and records discussion about its monorepo friction and its limits as a defense. The HN discussion of the GA release had 61 points and 11 comments; it debated whether staging reduces CI-takeover publication risk without being a complete supply-chain defense.
