---
source_url: https://fion.ac/jellyfish.pdf
ingested: 2026-10-10
sha256: f4cdfa406a6e56bd8682ae38a6cd00ce5b3a177afc0c952fb35e12cfddabcc0d
---
# Chen & Stratton — *Artificial Intelligence in the Firm: Bottlenecks in Software Production*

Fonte primária: https://fion.ac/jellyfish.pdf  
Versão lida: 2026-08-04; pesquisa tornada amplamente visível em cobertura técnica em 2026-10-09.

O working paper de Fiona Chen e James Stratton (Harvard) usa dados agregados e anonimizados da plataforma Jellyfish: aproximadamente 300 milhões de eventos de trabalho, 700 mil trabalhadores e 718 empresas entre janeiro de 2021 e março de 2026. O desenho é *staggered difference-in-differences* e explora o momento de adoção de assistentes e agentes de código; portanto, é evidência observacional em nível de firma, não um experimento aleatorizado nem um teste de um modelo/harness específico.

Para adoção de agentes, os autores estimam +30% em linhas de código, +20% em commits e +23% em pull requests. Não encontram aumento estatisticamente significativo na resolução de issues ou epics; também não observam aumento na complexidade média prevista de issues. O mecanismo proposto é revisão: o tempo de PR até merge cresce 49%, a fração de PRs que exige mudanças quase dobra, comentários por PR sobem 35% e a fração de pessoas fazendo review aumenta 14%.

O estudo não demonstra que agentes nunca aumentam a entrega nem que toda empresa terá o mesmo efeito: o recorte termina em março de 2026, a medição de adoção agrega ferramentas e a amostra vem de clientes Jellyfish. A conclusão reutilizável para desenho de workflows é mais estreita: taxa de geração de código não deve ser a métrica de sucesso; capacidade de revisão, evidência executável, taxa de aceitação, rework e tempo até mudança aceita precisam entrar no gargalo e na avaliação.

Corroboração independente: https://arstechnica.com/ai/2026/10/ai-coding-agents-generate-more-code-but-not-more-software/ — reportagem de 09/10 que descreve método, recorte e resultados, mas não é uma reprodução independente dos dados.
