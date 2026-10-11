# 24 — Glossário Git e GitHub

| Termo | Definição |
|---|---|
| Branch | Apontador móvel para um commit; linha de desenvolvimento ([[01-branches-switch-checkout\|guia]]) |
| Checkout | (Clássico) trocar branch ou repor ficheiros; hoje dividido em `switch`/`restore` |
| Cherry-pick | Copiar commits específicos para o HEAD atual ([[02-merge-rebase-cherry-pick\|guia]]) |
| Clone | Cópia completa de um repo remoto com histórico |
| Commit | Snapshot do projeto com hash, autor, data e mensagem |
| Conflito | Alterações incompatíveis que exigem decisão manual ([[01-conflitos-e-recuperacao\|guia]]) |
| Detached HEAD | HEAD apontado a um commit em vez de um branch |
| Fast-forward | Avanço de branch sem divergência, sem commit extra |
| Fetch | Trazer refs do remote sem tocar na working tree |
| Fork | Cópia de um repo na tua conta para contribuir via PR |
| HEAD | Apontador para a posição atual (branch/commit) |
| Hotfix | Branch de correção urgente a partir de `main` |
| Issue | Tarefa/bug/ideia numerada no GitHub (`#N`) |
| Main | Branch principal; em produção no nosso workflow |
| Merge | União de históricos (fast-forward ou merge commit) |
| Origin | Nome convencional do remote principal |
| Pull | `fetch` + integração no branch atual |
| Pull Request (PR) | Pedido de integração com review e CI ([[01-pull-requests-e-code-review\|guia]]) |
| Push | Enviar commits locais para o remote |
| Rebase | Reaplicar commits sobre nova base (reescreve hashes!) |
| Reflog | Diário local de movimentos do HEAD (rede de segurança) |
| Release | Tag + notas + artefactos de uma versão |
| Remote | Apelido de um repo noutro local (`origin`, `upstream`) |
| Reset | Mover branch para outro commit (`--soft/mixed/hard`) |
| Restore | Repor ficheiros (unstaging 🟢 / descartar edições 🟡) |
| Revert | Novo commit que desfaz outro (seguro após push) |
| SemVer | `MAJOR.MINOR.PATCH` ([[01-conventional-commits-semver-cicd\|guia]]) |
| Staging area (índice) | Seleção do próximo commit |
| Stash | Pilha temporária de trabalho a meio |
| Switch | Trocar branches (moderno) |
| Tag | Marca nomeada num commit (`v1.2.3`) |
| Upstream | Branch remoto seguido / repo original num fork |
| Working tree | Ficheiros no disco onde editas |

**Início:** [[README|Índice do guia]]
