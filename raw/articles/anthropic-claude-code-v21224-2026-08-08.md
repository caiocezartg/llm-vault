---
source_url: https://github.com/anthropics/claude-code/releases/tag/v2.1.224
ingested: 2026-08-08
sha256: 9c95eefe398cc583631b0ce94a21eb636c9a97ef7cbfdfb5e651c87ffbc37b62
---
# Claude Code v2.1.224: execução híbrida em infraestrutura própria e coordenação entre sessões

## Fonte primária

- Release oficial `v2.1.224`, publicada em 2026-08-07: https://github.com/anthropics/claude-code/releases/tag/v2.1.224
- Documentação de ambientes self-hosted: https://code.claude.com/docs/en/self-hosted-environments
- Documentação de mensagens entre sessões: https://code.claude.com/docs/en/cross-session-messaging

## Fatos verificáveis

A release adiciona `claude self-hosted-runner`, que permite a sessões do Claude Code iniciadas pela web, mobile e desktop executarem em máquinas ou containers operados pela organização. A capacidade está disponível em beta para planos Team e Enterprise; a release também adiciona instalação de plugins por arquivo HTTPS com pin opcional SHA-256, opções de mascaramento de credenciais estruturadas/JWT/AWS SigV4, e corrige um bypass de `denyRead` com barra final em macOS e Linux.

`SendMessage` e `ListAgents` permitem que sessões Claude Code em macOS e Linux descubram pares e troquem mensagens, inclusive entre máquinas. A mensagem não é uma via para aprovar permissões ou mudar configurações: uma ação que exija autorização continua exigindo a política de aprovação da sessão receptora.

## Limite de confiança e operação

O runner é execução híbrida, não inferência completamente self-hosted: checkout, artefatos e credenciais injetadas ficam na infraestrutura da organização, mas prompts, respostas, resultados de ferramentas, transcrições e inferência permanecem no plano de controle da Anthropic. Uma avaliação independente orienta usar runner efêmero com capacidade um, egress default-deny externo ao produto, credenciais curtas por sessão, bloqueio de metadata de cloud e teste de recuperação/perda de trabalho não commitado antes de qualquer rollout.

## Evidência independente

- DevelopersIO reproduziu `ListAgents`/`SendMessage`, confirmou entrega entre sessões e analisou as mudanças de sandbox: https://dev.classmethod.jp/en/articles/20260807-cc-updates-v2-1-224/
- Checklist técnico independente do DEV Community delimita o modelo híbrido, restrições de beta e controles de produção: https://dev.to/ahab_indieseek/claude-code-21224-self-hosted-environments-checklist-2ck9
