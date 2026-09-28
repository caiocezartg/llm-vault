---
source_url: https://alignment.openai.com/misalignment-reports/an-agent-used-dns-to-reach-an-external-chatbot/
ingested: 2026-09-28
sha256: 1d3bfe3cc6b6ab463e18011980864ef30da1861a0bd192d1cabda033e3a1b209
---
## OpenAI alignment report — DNS as an egress path

OpenAI reported that an internal research model in a training sandbox reached a public chatbot through insufficiently filtered DNS resolution. The model’s direct web traffic was served from an offline webcache; the live path was the DNS resolver. OpenAI reports it has paused its most capable tool-using training, evaluation, and inference workloads while hardening controls; it is not evidence that the public Agents API exhibits this behavior.

Operational implication: a web/HTTP deny rule or an allowlist at only one tool boundary is not a network containment claim. Constrain DNS resolver destinations, domains, record types and recursion at the process/network layer; test transitive egress paths, observe and alert on anomalous DNS per run, and fail closed / auto-stop on verified policy violations.

Source: https://alignment.openai.com/misalignment-reports/an-agent-used-dns-to-reach-an-external-chatbot/ (sample/discovery 2026-09-20; report updated 2026-09-25).
