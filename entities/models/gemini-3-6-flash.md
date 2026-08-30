---
title: Gemini Flash (3.6/3.7)
created: 2026-07-23
updated: 2026-08-14
type: entity
tags: [llm, model, inference, reasoning, tool-calling, agent, coding]
sources: [raw/articles/google-gemini-3-6-flash-2026-07-23.md, raw/articles/google-gemini-3-7-flash-2026-08-14.md]
confidence: medium
contested: false
contradictions: []
---

# Gemini Flash (3.6/3.7)

## Visão geral

A linha Gemini Flash é a opção proprietária de alta vazão da Google para fluxos multimodais, agentic e de coding. Gemini 3.6 Flash chegou em julho de 2026; Gemini 3.7 Flash, publicado em 13 de agosto, mantém a mesma função mas dobra a referência de preço introdutório por token em relação ao preço original do 3.6 e declara melhorias de engenharia. A disponibilidade por Gemini API e o rollout em Copilot tornam a linha um candidato de avaliação controlada para tarefas de engenharia, não um substituto automático para os modelos já roteados em [[comparisons/model-routing-hermes-opencode-pi]]. ^[raw/articles/google-gemini-3-6-flash-2026-07-23.md] ^[raw/articles/google-gemini-3-7-flash-2026-08-14.md]

## Fatos de integração e custo

A fonte primária do 3.6 anunciou Gemini API/AI Studio, Android Studio, Antigravity e Gemini Enterprise Agent Platform; o GitHub documentou rollout gradual no Copilot. Para 3.7, a Google documenta a Gemini API e preço de US$ 0,75 por 1M tokens de entrada e US$ 3,75 por 1M tokens de saída — metade do preço original de 3.6. O changelog do GitHub confirma rollout gradual no Copilot, incluindo VS Code, CLI, cloud agent, JetBrains e outras superfícies; admins Business/Enterprise precisam habilitar a política Preview. ^[raw/articles/google-gemini-3-7-flash-2026-08-14.md]

## Evidência e limites

A Google relata para 3.7 Flash ganhos contra 3.6 em FrontierCode e DeepSWE. A Artificial Analysis mede a variante `high` com índice 56, 340,1 tokens/s e contexto de 1M, o que sustenta uma triagem independente de preço/velocidade, mas não uma conclusão sobre sucesso, custo total ou segurança num harness específico. A discussão no Hacker News (738 pontos e 398 comentários no snapshot de 14/08) mostrou interesse técnico e fricções de onboarding/posição competitiva, não uma avaliação reproduzível de coding agents. ^[raw/articles/google-gemini-3-7-flash-2026-08-14.md]

## Adoção controlada

- Começar com tarefas curtas e repetíveis, mantendo o mesmo harness, testes ocultos e limite de custo/tempo para comparar contra o baseline.
- Medir conclusão verificável, diffs fora de escopo, chamadas de ferramenta, tokens, latência e retrabalho humano — não só benchmark do fornecedor.
- Tratar as afirmações de qualidade/custo como hipótese até reproduzir em tarefas próprias; usar a decisão de roteamento existente em [[comparisons/model-routing-hermes-opencode-pi]] e as salvaguardas de avaliação de [[entities/models/gpt-5-6]].

## Fontes

- [Google — Gemini 3.6 Flash](https://blog.google/innovation-and-ai/models-and-research/gemini-models/gemini-3-6-flash-3-5-flash-lite-3-5-flash-cyber/)
- [Google — Gemini 3.7 Flash](https://blog.google/innovation-and-ai/models-and-research/gemini-models/introducing-gemini-3-7-flash/)
- [Artificial Analysis — 3.7 Flash](https://artificialanalysis.ai/models/gemini-3-7-flash)
- [GitHub Copilot — rollout 3.7](https://github.blog/changelog/2026-08-13-gemini-3-7-flash-is-now-available-in-github-copilot/)
- [Hacker News — discussão 3.7](https://news.ycombinator.com/item?id=49289112)
