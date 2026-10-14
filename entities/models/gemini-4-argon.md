---
title: Gemini 4 Argon
created: 2026-10-01
updated: 2026-10-14
type: entity
tags: [llm, model, reasoning, coding, inference, evaluation, agent]
sources: [raw/articles/google-gemini-4-argon-2026-09-30.md, https://cloud.google.com/blog/products/ai-machine-learning/gemini-4-argon-available-on-google-cloud, https://www.reuters.com/business/google-launches-flagship-ai-model-gemini-4-argon-developers-businesses-2026-10-13/]
confidence: medium
contested: false
contradictions: []
---

# Gemini 4 Argon

## Estado e acesso

A Google anunciou Gemini 4 Argon em 30 de setembro de 2026 como modelo de fronteira para engenharia de software de longo horizonte, trabalho de conhecimento e defesa cibernética. O acesso inicial era limitado a defensores confiáveis via Fairwind e testadores iniciais. Em 13 de outubro, a Google tornou o modelo disponível via API paga, AI Studio, Gemini Enterprise e Antigravity, sob o ID `gemini-4-argon`; o GitHub também o disponibilizou gradualmente no Copilot para planos elegíveis. Portanto, a mudança de acesso é material: Argon agora pode entrar em um trial controlado, mas não deve virar rota padrão sem avaliação própria. ^[raw/articles/google-gemini-4-argon-2026-09-30.md]

## Fatos de integração e evidência

A fonte primária declara preço introdutório de US$2/M tokens de entrada e US$10/M de saída até 30 de novembro, com 95% de desconto para entrada em cache; depois a tabela sobe para US$4/M e US$20/M. A Google também reporta benchmarks e ganhos internos de engenharia, mas são evidências do fornecedor e não provam taxa de tarefas aceitas, custo total ou comportamento no harness de Caio. A disponibilidade comercial e o preço de lançamento foram confirmados independentemente pela Reuters. ^[raw/articles/google-gemini-4-argon-2026-09-30.md]

A atenção técnica inicial foi muito alta — 1.278 pontos e 818 comentários no Hacker News no snapshot de 01/10 —, mas a conversa contém relatos anedóticos e críticas de acesso/harness; não constitui benchmark independente. A base apropriada para um futuro trial continua sendo a comparação de rotas em [[comparisons/model-routing-hermes-opencode-pi]] e os critérios usados para [[entities/models/gemini-3-6-flash]].

## Trial quando houver acesso

- Fixar modelo/nível de esforço, provider, ferramentas, cache, orçamento e conjunto de tarefas retidas; comparar contra uma rota já disponível, como [[entities/models/gpt-6-sol-luna]].
- Medir taxa de tarefa aceita, testes e review, crescimento de contexto, cache-hit, latência, retries, erros de tool/schema e custo por resultado aceito.
- Manter privilégios de ferramentas, segredos, egress e aceitação final externos ao agente, conforme [[coding/architecture/merge-gated-dag-coding-workflow]].

## Fontes

- [Google — anúncio, acesso, preço e benchmarks declarados](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-4-argon/)
- [Google Cloud — GA, superfícies de acesso e preço](https://cloud.google.com/blog/products/ai-machine-learning/gemini-4-argon-available-on-google-cloud)
- [Reuters — disponibilidade global, preço e ressalvas](https://www.reuters.com/business/google-launches-flagship-ai-model-gemini-4-argon-developers-businesses-2026-10-13/)
- [GitHub Changelog — disponibilidade gradual no Copilot](https://github.blog/changelog/2026-10-13-gemini-4-argon-in-github-copilot)
- [Hacker News — discussão e sinal comunitário inicial](https://news.ycombinator.com/item?id=49913571)