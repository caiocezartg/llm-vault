---
title: NVIDIA OpenShell
created: 2026-10-02
updated: 2026-10-02
type: entity
tags: [agent, tool, workflow, coding, devops, testing]
sources: [raw/articles/nvidia-open-agent-safety-platform-2026-09-28.md]
confidence: medium
contested: false
contradictions: []
---

# NVIDIA OpenShell

## Estado e arquitetura

NVIDIA anunciou a Open Agent Safety Platform em 28 de setembro de 2026. Sua parte adotável por software é OpenShell: um runtime Apache-2.0 para agentes autônomos com sandbox, política YAML declarativa e isolamento de filesystem, processo, rede e credenciais. A documentação 0.1.x inclui Claude Code, OpenCode, Codex e GitHub Copilot CLI como casos de uso de coding agents. ^[raw/articles/nvidia-open-agent-safety-platform-2026-09-28.md]

A plataforma também descreve Sentry, um desenho opcional de monitoramento fora da banda em DPUs BlueField-4. A alegação de quarentena independente em milissegundos é de NVIDIA e depende de hardware específico; não deve ser convertida em promessa de contenção para ambientes sem essa arquitetura ou sem avaliação independente. ^[raw/articles/nvidia-open-agent-safety-platform-2026-09-28.md]

## O que é verificável e o que ainda exige trial

A documentação expõe controles concretos: Landlock para paths declarados, política de rede, identidade de processo sem privilégios, seccomp e resolução de credenciais opacas somente em endpoints autorizados. O repositório público tem 14,1 mil stars, 1,6 mil forks e atividade corrente no snapshot de 02/10; são sinais de interesse e maturidade de desenvolvimento, não auditoria de segurança. A discussão no Hacker News, com 227 pontos e 299 comentários, debateu precisamente o limite entre sandbox, utilidade e autoridade ampla.

## Aplicação para Hermes e coding agents

OpenShell é um candidato a piloto Linux para uma lane de agentes com privilégios estreitos, não uma autorização para executar repositórios ou ferramentas sem gates. Versionar e revisar a política junto do task packet; testar leitura de segredos, escrita fora de escopo, egress direto/transitivo, symlinks, sockets e comportamento de falha; e manter credenciais, aprovação e merge fora do sandbox. Isso complementa [[entities/tools/hermes-agent]], [[comparisons/model-routing-hermes-opencode-pi]] e [[coding/architecture/merge-gated-dag-coding-workflow]].

## Fontes

- [NVIDIA — anúncio da plataforma](https://nvidianews.nvidia.com/news/open-agent-safety-platform)
- [NVIDIA Docs — arquitetura e controles de OpenShell](https://docs.nvidia.com/openshell/latest/about/overview)
- [Repositório OpenShell](https://github.com/NVIDIA/OpenShell)
- [SecurityWeek — análise técnica independente](https://www.securityweek.com/nvidia-unveils-ai-agent-safety-platform-with-hardware-based-watchdog/)
- [Hacker News — discussão e ressalvas](https://news.ycombinator.com/item?id=49879883)