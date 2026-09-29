---
title: Workload Identity and Recovery Boundaries
created: 2026-09-29
updated: 2026-09-29
type: concept
tags: [agent, workflow, devops, architecture]
sources:
  - raw/articles/microsoft-storm-3168-2026-09-25.md
confidence: high
contested: false
contradictions: []
---

# Workload Identity and Recovery Boundaries

## Definition

Uma identidade de workload (por exemplo, service principal) autoriza software e automações a agir no plano de controle. Ela não deve ter autoridade implícita para apagar recursos, recuperar chaves e desabilitar a recuperação sem controles independentes, observáveis e reversíveis.

## Evidence and design rule

O relatório Microsoft de setembro de 2026 sobre Storm-3168 descreve duas identidades comprometidas que dividiram descoberta, exclusão e coleta de chaves no Azure. Locks de recurso e proteção de exclusão bloquearam parte das tentativas mesmo quando a identidade operacional tinha privilégios amplos. A evidência sustenta a regra de arquitetura, não a atribuição universal de autonomia: defesas de recuperação precisam sobreviver ao comprometimento do principal que opera o workload. ^[raw/articles/microsoft-storm-3168-2026-09-25.md]

Rotacionar ou revogar imediatamente segredos publicados, inclusive os removidos de issues ou commits; restringir RBAC a recursos/operações necessários; preferir credenciais efêmeras e escopadas por tarefa; e registrar leitura de chaves, picos de deleção e alterações em locks. Para agentes, o escopo de ferramenta não é suficiente: a identidade e a plataforma precisam negar operações irreversíveis fora de uma autorização independente. Esse limite complementa [[coding/architecture/merge-gated-dag-coding-workflow]] e a separação de egress/autoridade em [[entities/tools/openai-agents-api]].

## Practical verification

Executar periodicamente um exercício não produtivo de identidade comprometida: confirmar que o principal não consegue enumerar ou ler chaves fora do escopo, apagar backups/locks, ou exceder orçamento de operações. Validar alertas de `ListKeys`, exclusões em lote e modificações de recovery, além do percurso de revogação e restauração.

## Sources

- [Microsoft Security report](https://www.microsoft.com/en-us/security/blog/2026/09/25/storm-3168-agentic-driven-cloud-attacks-using-compromised-service-principals/)
- [Security Affairs independent coverage](https://securityaffairs.com/199905/cyber-crime/storm-3168-linked-to-jadepuffer-abused-stolen-azure-identities.html)
