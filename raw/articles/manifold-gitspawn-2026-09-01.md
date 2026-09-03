---
source_url: https://www.manifold.security/blog/ai-coding-agents-git-hijack
ingested: 2026-09-03
sha256: d87a2092cd842e2d4a92fa7e6d98b6356351f93c529ff3a36ef8d5ca47c997b1
---
# GitSpawn — pesquisa Manifold Security

Publicado: 2026-09-01
Fonte primária: https://www.manifold.security/blog/ai-coding-agents-git-hijack

A pesquisa GitSpawn relata que agentes de coding podem executar comandos Git para coletar contexto de um repositório. Quando o repositório chega como diretório com .git, por exemplo em ZIP, drive compartilhado, sincronização ou USB, a configuração local core.fsmonitor pode fazer Git executar um comando no host durante a atualização de índice. O texto afirma que isso ocorre antes de prompt de confiança ou aprovação em produtos afetados.

O relatório identifica oito achados em sete agentes e diz que quatro continuavam sem patch na publicação. Para Hermes Agent, descreve git status com configuração do repositório não sanitizada; o achado foi reconfirmado na versão 0.21.0 em 2026-09-01, recebeu CVE-2026-71963 por VulnCheck e permanecia sem patch segundo a fonte.

A conclusão operacional reutilizável é que a configuração Git de um diretório recebido não deve ser tratada como inerte quando uma ferramenta autônoma invoca Git. Repositórios não confiáveis devem ser obtidos por clone novo de URL confiável ou abertos primeiro em ambiente isolado, com credenciais e egress mínimos.