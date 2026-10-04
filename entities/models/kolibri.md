---
title: Kolibri
created: 2026-10-04
updated: 2026-10-04
type: entity
tags: [llm, model, open-weight, inference, reasoning, tool-calling, evaluation]
sources: [raw/articles/aleph-alpha-kolibri-2026-10-03.md]
confidence: medium
contested: false
contradictions: []
---

# Kolibri

## Estado e superfície

Kolibri é o modelo MoE bilíngue alemão/inglês da Aleph Alpha, lançado com pesos Apache-2.0 em 3 de outubro de 2026. O card declara 78B parâmetros totais, 3,46B ativos por token, raciocínio explícito, tool calling e até 1M de contexto; o próprio fornecedor recomenda até 262k tokens para eficiência e tarefas complexas. A rota de serving publicada é um plugin de vLLM, não uma integração pronta para Hermes ou um atalho para autonomia segura. ^[raw/articles/aleph-alpha-kolibri-2026-10-03.md]

O custo computacional por token pode ser baixo para o tamanho, mas a memória não: os pesos FP8 ocupam cerca de 78 GB e o card lista ao menos 2× A100 80 GB ou hardware de classe H200/B200/B300. Portanto, é um candidato de laboratório para inferência auto-hospedada e privacidade de dados, não um modelo local leve nem um substituto imediato para rotas API. ^[raw/articles/aleph-alpha-kolibri-2026-10-03.md]

## Evidência e limite de adoção

A Aleph Alpha publica pesos, card, relatório técnico e comparativos para código, raciocínio e tarefas agentic; estes resultados continuam sendo evidência do fornecedor. A discussão inicial no Hacker News registrou 546 pontos e 308 comentários no snapshot de 4 de outubro, com atenção à abertura do relatório e questionamentos sobre dados, licença e extrapolação de benchmark. Isso é sinal de interesse técnico, não validação independente de taxa de sucesso, custo ou confiabilidade em um harness de coding.

O próprio card posiciona o modelo para colaboração humana e afirma que o sistema chamador deve validar resultados. A fronteira permanece a mesma de [[entities/models/muse-glimmer]] e [[entities/models/lfm25-26b]]: pesos abertos melhoram portabilidade e residência de dados, mas não concedem autoridade sobre ferramentas, rede, credenciais ou merge.

## Trial controlado

Só testar se houver hardware compatível e com um endpoint descartável. Fixar versão de pesos, plugin vLLM, quantização, parser de reasoning/tool calling, contexto e concorrência; comparar contra uma rota existente com tarefas retidas. Medir sucesso aceito, correção de schema/tool calls, prefill/decode, memória, energia, recuperação de falhas, custo e resultados de CI/revisão. Preservar sandboxes, egress mínimo e gates externos conforme [[comparisons/model-routing-hermes-opencode-pi]].

## Fontes

- [[raw/articles/aleph-alpha-kolibri-2026-10-03]]
- https://huggingface.co/Aleph-Alpha/Kolibri-1
- https://news.ycombinator.com/item?id=49942706
