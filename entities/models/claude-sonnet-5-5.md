---
title: Claude Sonnet 5.5
created: 2026-09-29
updated: 2026-09-29
type: entity
tags: [llm, model, reasoning, tool-calling, context-window, coding, evaluation, inference]
sources:
  - raw/articles/anthropic-claude-sonnet-5-5-2026-09-28.md
confidence: medium
contested: false
contradictions: []
---

# Claude Sonnet 5.5

## Overview

Anthropic lançou `claude-sonnet-5-5` em 28 de setembro de 2026 como a rota Sonnet para tarefas diárias bem delimitadas, correção de bugs e iteração rápida. A tabela publicada mantém US$2/M tokens de entrada, US$10/M de saída e US$0,20/M de cache reads; a empresa afirma geração 30%+ mais rápida e até 30% menos custo por tarefa do que Sonnet 5. ^[raw/articles/anthropic-claude-sonnet-5-5-2026-09-28.md]

## Capability and compatibility boundary

A Anthropic reporta 70,6% em Terminal-Bench 4.0, 46,2% em FrontierCode 1.1 Main a Max effort e 55,5% em CursorBench 4.0. Esses são dados de lançamento, não uma decisão de rota: o próprio anúncio preserva [[entities/models/claude-opus-5-5]] como opção mais forte para julgamento sustentado e trabalho complexo aberto. Integrações que desligavam thinking devem migrar para `between_tools`; disponibilidade é declarada para Claude Platform, AWS, Google Cloud e Azure. ^[raw/articles/anthropic-claude-sonnet-5-5-2026-09-28.md]

## Cost-per-accepted-task trial

Uma avaliação independente da Artificial Analysis encontrou grande melhora de capacidade em Max effort, mas também aproximadamente 193 mil tokens de saída por tarefa do seu Intelligence Index e cerca de US$7,60 por tarefa — uma ressalva contra inferir economia a partir de preço por token. Medir em tarefas retidas com harness, tool policy, cache, isolamento e orçamento fixos: modelo efetivo/fallback, effort, tokens, tool calls, latência, custo por tarefa aceita, testes, revisão e diffs fora de escopo. A autoridade de aceitação e os controles externos continuam em [[comparisons/model-routing-hermes-opencode-pi]] e [[coding/architecture/merge-gated-dag-coding-workflow]].

## Sources

- [Anthropic announcement](https://www.anthropic.com/claude-sonnet-5-5)
- [Artificial Analysis evaluation](https://artificialanalysis.ai/articles/claude-sonnet-5-5)
- [Hacker News discussion](https://news.ycombinator.com/item?id=49881850)
