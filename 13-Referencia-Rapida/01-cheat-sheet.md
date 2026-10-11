# 22 — Referência rápida

> **Nível:** todos · **Uso:** uma página para o dia a dia. Detalhe em cada nota ligada.
> **Como ler:** corre `status` antes e depois de tudo; respeita os selos [SEGURO]/[ATENCAO]/[DESTRUTIVO].

## Diário

```bash
git status --short
git pull --ff-only                    # atualizar (seguro)
git add -p                            # preparar por partes
git commit -m "feat(escopo): descricao"
git push
git log --oneline --graph --decorate -10
```

Detalhe: [[01-init-clone-status-add-commit|05]] · [[02-log-diff-show|06]] · [[01-repositorios-remotes-tags|10]]

## Branches e integração

```bash
git switch -c feature/x               # criar + trocar
git switch main | git switch -        # trocar / voltar atrás
git branch -d feature/x               # apagar (merged)
git merge feature/x                   # integrar (seguro)
git rebase main                       # atualizar feature privada ([ATENCAO]: nunca em partilhado)
git cherry-pick <hash>                # trazer commit pontual ([ATENCAO])
```

Detalhe: [[01-branches-switch-checkout|08]] · [[02-merge-rebase-cherry-pick|09]]

## Sincronizar / desfazer

```bash
git fetch --prune origin              # observar + limpar fantasmas
git stash push -m "wip" && git stash pop   # guardar/recuperar a meio
git restore --staged <f>              # tirar do staging [SEGURO]
git restore <f>                       # descartar edições [ATENCAO]: confirma diff antes
git revert <hash>                     # desfazer commit partilhado [SEGURO]
git reset --soft HEAD~1               # refazer último commit local [ATENCAO]
git reflog                            # achar commits perdidos [SEGURO]
```

Detalhe: [[03-gitignore-stash-restore|07]] · [[01-reset-revert-reflog|16]] · [[02-fetch-pull-push-remote-avancado|17]]

## GitHub: publicar, versionar, colaborar

```bash
git push -u origin feature/x          # publicar + tracking
git tag -a v1.2.3 -m "Release" && git push origin v1.2.3
# PR: push → GitHub → Compare & pull request → review → merge → delete branch
# Fecha issue: "Closes #12" na descrição do PR
```

Detalhe: [[02-GitHub-Issues-releases-actions|11]] · [[01-pull-requests-e-code-review|12]] · [[01-conventional-commits-semver-cicd|18]]

## Tabela de risco

| [SEGURO] | [ATENCAO] | [DESTRUTIVO] |
|---|---|---|
| status, log, diff, show, fetch, stash push/pop, revert, reflog, merge | rebase, reset --soft/mixed, commit --amend (local), cherry-pick, push --force-with-lease | reset --hard, branch -D, stash drop, push --force, filter-repo, apagar `.git` |

**Antes de [ATENCAO]/[DESTRUTIVO]:** `git status` + `git branch --show-current` + `git stash list`.

## Auto-teste de 60 segundos

1. Onde estou e o que mudou? (`status --short`, `branch --show-current`)
2. O que vai no próximo commit? (`diff --staged`)
3. O remoto tem novidades? (`fetch` + `log main..origin/main`)

**Detalhe:** [[01-glossario|24 — Glossário]] · [[01-erros-comuns-e-solucoes|21 — Erros]] · [[README|Índice]]
