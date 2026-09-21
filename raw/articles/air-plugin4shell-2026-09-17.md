---
source_url: https://www.air.security/blog-posts/plugin4shell
ingested: 2026-09-21
sha256: 88b79ea7098da4691b602ac7ccd5f2d27dfa448ef1a1cf3dd7bc16af2ecfd48c
---
# Plugin4Shell — AIR Security disclosure excerpt

Source: https://www.air.security/blog-posts/plugin4shell
Published: 2026-09-17

## Summary

Plugin4Shell is described as a zero-click RCE in the plugin-install flows of Claude Code, Codex, GitHub Copilot, and Gemini CLI. AIR reports that a marketplace can pin a reviewed commit while the client later resolves a different ref with the same apparent identity, so attacker-controlled code can reach the working tree. The report says the affected client must be updated; marketplace review and commit pinning alone do not restore the integrity boundary.

## Technical mechanism reported by AIR

For Claude Code, Codex, and GitHub Copilot, AIR describes a client that clones the plugin repository and runs `git checkout <pinned SHA>` without verifying the resulting `HEAD`. If the repository host permits a default branch named exactly as the 40-hex commit identifier, Git resolves the ref name in preference to the object ID. AIR says background plugin updates make this path zero-click for already-installed plugins.

For Gemini CLI, AIR describes a distinct collision: the client fetches the pinned commit but checks out `FETCH_HEAD`; a default branch with that name can resolve instead. AIR proposes verifying the resolved working-tree commit after checkout: `git rev-parse HEAD` must equal the pinned SHA, otherwise installation aborts.

## Reported remediation status

AIR reports that Anthropic patched Claude Code in `2.1.179` and OpenAI patched Codex in `0.146.0`; Microsoft had not shipped a GitHub Copilot fix, and Google had deprecated Gemini CLI without a patch. These vendor-status claims were independently reported by The Hacker News and should be rechecked before operational use.

## Durable boundary

A source pin is a claim about intended content, not proof that the content actually executed. Any agent client that installs a plugin, skill, or executable from Git must verify the checked-out commit after ref resolution, then retain external controls: provenance review, scoped filesystem/network/credential authority, isolation, and independent repository gates.
