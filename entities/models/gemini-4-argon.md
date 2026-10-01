---
title: Gemini 4 Argon
created: 2026-10-01
updated: 2026-10-01
type: entity
tags: [llm, model, reasoning, coding, inference, evaluation, agent]
sources: [raw/articles/google-gemini-4-argon-2026-09-30.md]
confidence: medium
contested: false
contradictions: []
---

# Gemini 4 Argon

## Estado e acesso

A Google anunciou Gemini 4 Argon em 30 de setembro de 2026 como modelo de fronteira para engenharia de software de longo horizonte, trabalho de conhecimento e defesa cibernética. No anúncio, o acesso ainda está limitado a defensores confiáveis via Fairwind e testadores iniciais; API, empresas e consumidores são uma etapa futura. Portanto, Argon é um candidato a acompanhar e preparar para avaliação — não uma rota disponível para adoção imediata. ^[raw/articles/google-gemini-4-argon-2026-09-30.md]

## Fatos de integração e evidência

A fonte primária declara 1M de tokens de saída e preço introdutório de US$2/M tokens de entrada, US$10/M de saída e 95% de desconto para entrada em cache; após o período inicial, a tabela prevista sobe para US$4/M e US$20/M. A Google também reporta 77,9% em DeepSWE v1.1 e resultados internos de migração/otimização, mas são evidências do fornecedor e não provam taxa de tarefas aceitas, custo total ou comportamento no harness de Caio. ^[raw/articles/google-gemini-4-argon-2026-09-30.md]

A atenção técnica inicial foi muito alta — 1.278 pontos e 818 comentários no Hacker News no snapshot de 01/10 —, mas a conversa contém relatos anedóticos e críticas de acesso/harness; não constitui benchmark independente. A base apropriada para um futuro trial continua sendo a comparação de rotas em [[comparisons/model-routing-hermes-opencode-pi]] e os critérios usados para [[entities/models/gemini-3-6-flash]].

## Trial quando houver acesso

- Fixar modelo/nível de esforço, provider, ferramentas, cache, orçamento e conjunto de tarefas retidas; comparar contra uma rota já disponível, como [[entities/models/gpt-6-sol-luna]].
- Medir taxa de tarefa aceita, testes e review, crescimento de contexto, cache-hit, latência, retries, erros de tool/schema e custo por resultado aceito.
- Manter privilégios de ferramentas, segredos, egress e aceitação final externos ao agente, conforme [[coding/architecture/merge-gated-dag-coding-workflow]].

## Fontes

- [Google — anúncio, acesso, preço e benchmarks declarados](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-4-argon/)
- [Hacker News — discussão e sinal comunitário inicial](https://news.ycombinator.com/item?id=49913571)