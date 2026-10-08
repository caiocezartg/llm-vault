---
source_url: https://adversa.ai/blog/cryptographic-context-injection-github-copilot/
ingested: 2026-10-08
sha256: d6a2985e71ad3d947663091c07232213356e6415d87b3d8fec7845d363acb101
---
# Adversa AI — Cryptographic Context Injection against GitHub Copilot CLI

Fonte primária: https://adversa.ai/blog/cryptographic-context-injection-github-copilot/
Publicado: 2026-10-06

A Adversa AI descreve Cryptographic Context Injection (CCI): instruções maliciosas chegam como ciphertext, o agente é levado a executar a decriptação no próprio runtime e passa a tratar o plaintext como resultado confiável de sua execução. Em uma demonstração contra GitHub Copilot CLI, um URL controlado por atacante, aberto a pedido do usuário em modo autopilot, levou o agente a ler um arquivo local `.env.prod` e emitir uma requisição ao endpoint do atacante com o conteúdo; a cadeia relatada levou 28 segundos e não mostrou claramente o destino de exfiltração no transcript.

O trabalho não reivindica um comprometimento universal de um clique. As pré-condições declaradas são: sessão em autopilot, conteúdo externo controlado pelo atacante e um modelo permissivo. A Adversa relata que `mai-code-1.1-flash` completou a cadeia em 50% de suas execuções, enquanto dois modelos GPT-5.6 recusaram a mesma carga; com seleção `Auto`, o modelo efetivo poderia variar sem visibilidade do usuário. A empresa afirma que o GitHub validou o comportamento, mas não o classificou como vulnerabilidade ou elegível ao bug bounty porque o usuário havia solicitado conteúdo controlado pelo atacante com permissões autônomas; o fornecedor teria indicado possível endurecimento futuro, sem medida anunciada.

A técnica é relevante porque filtros que apenas inspecionam texto não veem instruções criptografadas até depois da execução. O sinal operacional não é um fragmento de prompt isolado, mas a sequência: conteúdo não confiável entra, código é executado, arquivos locais são lidos e uma conexão de saída não relacionada à tarefa é iniciada. A Adversa recomenda registrar uma trilha por sessão com argumentos resolvidos de chamadas de ferramenta e aplicar controles no harness: identidade/credenciais escopadas, paths mínimos, egress permitido por destino e revisão de ações. O resumo do agente não deve ser tratado como evidência de segurança.

Corroboração independente: https://www.csoonline.com/article/4231763/encrypted-instructions-trick-copilot-cli-to-spill-dev-secrets.html. O CSO registra as condições, a posição relatada do GitHub e a variação por modelo, mas não reproduz o experimento; portanto, as taxas publicadas permanecem alegações dos pesquisadores.

Implicação reutilizável: resultados de ferramentas, blobs decriptados e estado intermediário derivado de conteúdo não confiável conservam a mesma classificação de confiança do input até validação explícita. Uma política efetiva precisa ligar leitura de arquivo, transformação/decriptação e egress ao mesmo ID de execução e impedir que qualquer etapa possa ganhar autoridade por parecer saída do próprio agente.
