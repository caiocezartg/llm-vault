---
source_url: https://github.com/microsoft/mxc/releases/tag/v1.0.0
ingested: 2026-10-11
sha256: e2e7570451fee6a3877e140000dadb8f449079bb310184dcea154f0378b68b10
---
# Microsoft Execution Containers (MXC) SDK v1.0.0

Primary-source excerpt captured for durable containment analysis.

Microsoft released MXC SDK v1.0.0 on 7 October 2026 as the first stable SDK surface for Rust, .NET and Node.js. The release defines explicit V1 entrypoints and says the 1.x public boundary will follow semantic versioning. Its API surface covers provisioning/lifecycle operations, direct execution with captured output, streams or a PTY, backend/capability discovery, filesystem-policy construction and Windows telemetry-consent management.

Microsoft’s accompanying general-availability announcement describes MXC as a policy-driven layer that keeps filesystem, network, UI and process constraints outside the agent workload. It documents distinct backends: process containers on Windows/macOS/Linux; a Windows-only session container with separate account/session/desktop boundaries; Windows-only WSL containers; and experimental MicroVMs on Windows and Linux. The backend selection changes the isolation semantics.

The announcement further describes enforcement, learning and permissive modes. On Windows process containers, learning blocks ungranted access and records it, while permissive allows the operation but records what a policy would deny. This is a policy-authoring aid, not a security result: policies must be exercised under enforcement, and every backend’s guarantees must be evaluated separately.

The SDK/repository establishes an implementation artifact but not an independent security audit. The public Hacker News discussion of the 1.0 release included substantive skepticism about documentation quality, cross-backend abstraction and egress/identity gaps. Treat the project as a controlled-pilot candidate and validate filesystem, network, credential, process, UI and failure boundaries on the specific host/backend.

Primary release: https://github.com/microsoft/mxc/releases/tag/v1.0.0
Official GA announcement: https://blogs.windows.com/windowsdeveloper/2026/10/07/microsoft-execution-containers-policy-driven-containment-for-ai-agents/
Published: 2026-10-07
Captured: 2026-10-11
