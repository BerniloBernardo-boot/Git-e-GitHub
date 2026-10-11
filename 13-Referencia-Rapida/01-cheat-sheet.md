# 22 — Referência rápida ⚡

> Uma página para o dia a dia. Detalhe em cada nota ligada.

## Diário

```bash
git status --short
git pull --ff-only                    # atualizar (seguro)
git add -p                            # stagediar por partes
git commit -m "feat(escopo): descricao"
git push
git log --oneline --graph --decorate -10
```

## Branches

```bash
git switch -c feature/x               # criar + trocar
git switch main | git switch -        # trocar / voltar atrás
git branch -d feature/x               # apagar (merged)
git merge feature/x                   # integrar (seguro)
git rebase main                       # atualizar feature privada (🟡 nunca em partilhado)
```

## Sincronizar / desfazer

```bash
git fetch --prune origin
git stash push -m "wip" && git stash pop
git restore --staged <f>              # unstaging 🟢
git restore <f>                       # descartar edições 🟡
git revert <hash>                     # desfazer commit partilhado 🟢
git reset --soft HEAD~1               # refazer último commit local 🟡
git reflog                            # achar commits perdidos 🟢
```

## GitHub

```bash
git push -u origin feature/x          # publicar + tracking
git tag -a v1.2.3 -m "Release" && git push origin v1.2.3
# PR: push → GitHub → Compare & pull request → review → merge → delete branch
# Fecha issue: "Closes #12" na descrição do PR
```

## Tabela de risco

| 🟢 Seguro | 🟡 Cuidado | 🔴 Destrutivo |
|---|---|---|
| status, log, diff, show, fetch, stash push/pop, revert, reflog, merge | rebase, reset --soft/mixed, commit --amend (local), cherry-pick, push --force-with-lease | reset --hard, branch -D, stash drop, push --force, filter-repo, apagar `.git` |

**Detalhe:** [[01-glossario|Glossário]] · [[01-erros-comuns-e-solucoes|Erros]] · [[README|Índice]]
