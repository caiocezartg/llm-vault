---
source_url: https://www.microsoft.com/en-us/security/blog/2026/09/25/storm-3168-agentic-driven-cloud-attacks-using-compromised-service-principals/
ingested: 2026-09-29
sha256: 894ba71ec30311cc09b4227647a28a70de909f6ccd37dbc0c0aebd93ba107553
---

# Microsoft Security — Storm-3168 e service principals comprometidos (captura delimitada)

Em 25 de setembro de 2026, Microsoft associou atividade destrutiva em Azure ao ator JADEPUFFER, acompanhado como Storm-3168. Dois service principals comprometidos no mesmo tenant dividiram descoberta, destruição e coleta de credenciais. A Microsoft observou mais de 150 operações destrutivas ou de coleta em 35 minutos; a sequência destrutiva durou aproximadamente sete minutos e incluiu mais de 100 tentativas de exclusão de contas de storage.

O relatório descreve exclusões de Key Vault, Function App e App Service plan, tentativas contra bancos Azure SQL e contra locks de Azure Site Recovery/Azure Backup. Locks de recursos e proteção contra exclusão impediram uma parte das deleções. Cerca de 30 minutos depois, a identidade consultou chaves de mais de 30 storage accounts com `ListKeys`.

A Microsoft não confirma o vetor inicial. Ela informa, contudo, que client ID, client secret e tenant ID haviam sido publicados em texto simples em um issue público do GitHub e continuavam acessíveis pelo histórico de edição. A orientação explícita é tratar segredo exposto publicamente como comprometido e revogar ou rotacionar imediatamente, pois remover o conteúdo não o invalida.

Fonte primária: https://www.microsoft.com/en-us/security/blog/2026/09/25/storm-3168-agentic-driven-cloud-attacks-using-compromised-service-principals/
