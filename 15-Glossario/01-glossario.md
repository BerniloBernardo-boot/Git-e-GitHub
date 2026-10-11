# 24 — Glossário Git e GitHub

> **Nível:** todos · **Uso:** consulta rápida. Cada termo tem definição de 1 linha + ligação para a lição completa.
> **Como estudar:** tapa a coluna de definição e tenta definir cada termo em voz alta antes de ler.

| Termo | Definição |
|---|---|
| Branch | Apontador móvel para um commit; linha de desenvolvimento ([[01-branches-switch-checkout|08]]) |
| Checkout | Clássico: trocar branch ou repor ficheiros; hoje dividido em `switch`/`restore` ([[01-branches-switch-checkout|08]]) |
| Cherry-pick | Copiar commits específicos para o HEAD atual ([[02-merge-rebase-cherry-pick|09]]) |
| Clone | Cópia completa de um repo remoto com histórico ([[01-init-clone-status-add-commit|05]]) |
| Commit | Snapshot do projeto com hash, autor, data e mensagem ([[01-init-clone-status-add-commit|05]]) |
| Conflito | Alterações incompatíveis que exigem decisão manual ([[01-conflitos-e-recuperacao|13]]) |
| Detached HEAD | HEAD apontado a um commit em vez de um branch ([[01-branches-switch-checkout|08]]) |
| Fast-forward | Avanço de branch sem divergência, sem commit extra ([[02-merge-rebase-cherry-pick|09]]) |
| Fetch | Trazer refs do remote sem tocar na working tree ([[01-repositorios-remotes-tags|10]]) |
| Fork | Cópia de um repo na tua conta para contribuir via PR ([[02-fetch-pull-push-remote-avancado|17]]) |
| HEAD | Apontador para a posição atual (branch/commit) ([[01-O-que-e-Git-e-GitHub|01]]) |
| Hotfix | Branch de correção urgente a partir de `main` ([[02-Workflow-Cuidar-Angola|15]]) |
| Issue | Tarefa/bug/ideia numerada no GitHub (`#N`) ([[02-GitHub-Issues-releases-actions|11]]) |
| Main | Branch principal; produção neste guia ([[01-git-flow-github-flow-trunk-based|14]]) |
| Merge | União de históricos (fast-forward ou merge commit) ([[02-merge-rebase-cherry-pick|09]]) |
| Origin | Nome convencional do remote principal ([[01-repositorios-remotes-tags|10]]) |
| Pull | `fetch` + integração no branch atual ([[01-repositorios-remotes-tags|10]]) |
| Pull Request (PR) | Pedido de integração com review e CI ([[01-pull-requests-e-code-review|12]]) |
| Push | Enviar commits locais para o remote ([[01-repositorios-remotes-tags|10]]) |
| Rebase | Reaplicar commits sobre nova base (reescreve hashes) ([[02-merge-rebase-cherry-pick|09]]) |
| Reflog | Diário local de movimentos do HEAD; rede de segurança ([[01-reset-revert-reflog|16]]) |
| Release | Tag + notas + artefactos de uma versão ([[02-GitHub-Issues-releases-actions|11]]) |
| Remote | Apelido de um repo noutro local (`origin`, `upstream`) ([[01-repositorios-remotes-tags|10]]) |
| Reset | Mover branch para outro commit (`--soft/mixed/hard`) ([[01-reset-revert-reflog|16]]) |
| Restore | Repor ficheiros (unstaging [SEGURO] / descartar edições [ATENCAO]) ([[03-gitignore-stash-restore|07]]) |
| Revert | Novo commit que desfaz outro; seguro após push ([[01-reset-revert-reflog|16]]) |
| SemVer | `MAJOR.MINOR.PATCH` ([[01-conventional-commits-semver-cicd|18]]) |
| Staging area (índice) | Seleção do próximo commit ([[01-O-que-e-Git-e-GitHub|01]]) |
| Stash | Pilha temporária de trabalho a meio ([[03-gitignore-stash-restore|07]]) |
| Switch | Trocar branches (moderno) ([[01-branches-switch-checkout|08]]) |
| Tag | Marca nomeada num commit (`v1.2.3`) ([[01-repositorios-remotes-tags|10]]) |
| Upstream | Branch remoto seguido / repo original num fork ([[02-fetch-pull-push-remote-avancado|17]]) |
| Working tree | Ficheiros no disco onde editas ([[01-O-que-e-Git-e-GitHub|01]]) |

## Auto-teste (5 minutos)

1. Define sem ler: staging area, HEAD, upstream, fast-forward, revert.
2. Para cada um, diz o comando que o mostra ou manipula.
3. Escolhe 3 termos e explica-os a um colega com uma analogia.

**Início:** [[README|Índice do guia]]
