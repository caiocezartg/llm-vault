---
title: OpenAI Dots
created: 2026-10-02
updated: 2026-10-02
type: entity
tags: [agent, tool, workflow, llm, coding]
sources: [raw/articles/openai-dots-2026-09-29.md]
confidence: medium
contested: false
contradictions: []
---

# OpenAI Dots

## Estado e superfície

OpenAI anunciou Dots em 29 de setembro de 2026: agentes persistentes, alimentados por GPT-6 Astra, com computador e navegador próprios na nuvem. Um Dot pode acompanhar objetivos de modo assíncrono e levar contexto entre ChatGPT, Slack e Teams; o lançamento começa em mercados elegíveis para Pro e Business Premium, enquanto Enterprise depende de ativação beta pelo administrador. Portanto, é uma superfície gerenciada a avaliar, não um bloco de construção portátil para um workflow local. ^[raw/articles/openai-dots-2026-09-29.md]

## Controles e limites

A fonte primária declara que pesquisa proativa em apps conectados é somente leitura, que ações passam por checagens e que o ambiente de execução é separado dos sistemas que coordenam o agente e aplicam salvaguardas. A documentação também reconhece que Dots pode errar. O exemplo de converter feedback em mudanças testadas e PRs é uma demonstração do fornecedor, não evidência de confiabilidade de coding nem de aceitação em um repositório real. ^[raw/articles/openai-dots-2026-09-29.md]

A discussão inicial no Hacker News alcançou 763 pontos e 639 comentários no snapshot de 02/10. Ela trouxe relatos anedóticos de agentes persistentes em suporte, backlog e CI, mas também debateu custo, privacidade, supervisão e o risco de tratar agentes como software determinístico. Isso é sinal de interesse e escrutínio, não benchmark independente.

## Implicação para workflows

Dots reforça a separação entre memória/sessão persistente e autoridade de execução. Qualquer teste deve fixar um escopo reversível, usar ambiente e credenciais segregados, e manter especificação, prova de testes, revisão e merge fora da memória do agente, conforme [[coding/architecture/project-memory-and-multi-model-handoff-layers]] e [[coding/architecture/merge-gated-dag-coding-workflow]]. Para trabalho com modelo OpenAI, a comparação deve preservar a fronteira entre produto gerenciado, API e harness em [[entities/models/gpt-6-astra]] e [[entities/tools/openai-agents-api]].

## Fontes

- [OpenAI — anúncio e disponibilidade](https://openai.com/index/introducing-dots/)
- [OpenAI — controles, workspace e limites declarados](https://openai.com/index/how-we-build-safety-security-and-privacy-into-dots/)
- [Hacker News — discussão e sinal comunitário](https://news.ycombinator.com/item?id=49896604)