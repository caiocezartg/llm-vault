---
title: Microsoft Execution Containers
created: 2026-10-11
updated: 2026-10-11
type: entity
tags: [tool, agent, coding, devops, architecture]
sources:
  - raw/articles/microsoft-mxc-v1-2026-10-07.md
  - https://github.com/microsoft/mxc/releases/tag/v1.0.0
  - https://blogs.windows.com/windowsdeveloper/2026/10/07/microsoft-execution-containers-policy-driven-containment-for-ai-agents/
confidence: medium
contested: false
contradictions: []
---

# Microsoft Execution Containers (MXC)

Microsoft Execution Containers is an MIT-licensed, policy-driven execution SDK for containing untrusted or dynamically generated workloads, including coding-agent harnesses, tools and generated code. Version 1.0.0 (7 October 2026) establishes its stable Rust, .NET and Node.js SDK surface, with semver promised for the 1.x line. ^[raw/articles/microsoft-mxc-v1-2026-10-07.md]

## What it makes explicit

MXC moves the authority definition outside the agent process: a workload requests a container with explicit filesystem, process, network and UI permissions; the selected backend enforces what it can. The same high-level policy does **not** make every backend equivalent: process containment spans Windows/macOS/Linux, a Windows session container adds a distinct user/session/desktop boundary, Windows has WSL containers, and MicroVM support on Windows/Linux remains experimental. ^[raw/articles/microsoft-mxc-v1-2026-10-07.md]

The V1 SDK supports container lifecycle management and three interaction styles: run-to-completion with captured output, piped streams, and PTY-backed sessions where a backend supports them. Windows process containers also offer learning (deny and record) and permissive (allow but record) modes for policy discovery. These modes are for authoring a policy; acceptance requires retesting the final policy under enforcement. ^[raw/articles/microsoft-mxc-v1-2026-10-07.md]

## Adoption boundary

MXC is a concrete candidate for a Windows-oriented coding-agent pilot, especially where policy needs to remain inspectable and separate from the harness. It is not a portable proof of containment, and its general-availability announcement does not replace backend-specific escape testing, egress validation, credential isolation, repository-native gates or independent merge review. Public technical discussion around 1.0 highlighted uncertainty about the cross-backend abstraction and documentation, so the confidence applies to artifact availability rather than security efficacy.

A narrow pilot should pin the SDK/backend/policy, start with a synthetic repository and no valuable credentials, exercise allowed and denied path/process/network/UI behavior, record policy denials by run, then move the exact policy to enforcement. Use an isolated VM or stronger backend for unattended or higher-risk work; do not infer VM-level guarantees from a process-container configuration.

## Related

- [[coding/architecture/merge-gated-dag-coding-workflow]] — MXC can supply a policy-enforced execution boundary; it does not own task acceptance or merge authority.
- [[entities/tools/nvidia-openshell]] — OpenShell and MXC both aim to place enforcement outside the agent, but their backends and guarantees need separate validation.
- [[entities/tools/hermes-agent]] — Hermes remains responsible for bounded task orchestration and independent gates around any executor.
