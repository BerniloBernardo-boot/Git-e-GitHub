# 21 — Erros comuns e soluções

> Consulta rápida por mensagem de erro. **Selo** indica risco da solução.

## Autenticação e ligação

| Erro | Causa | Solução |
|---|---|---|
| `Permission denied (publickey)` | SSH sem chave/autorização | [[02-SSH-e-autenticacao#2-ssh-passo-a-passo-linux|Configurar SSH]] |
| `Support for password authentication was removed` | Password no HTTPS | Usar PAT |
| `repository not found` | URL errado / sem acesso | Confirma URL + acesso; `git remote -v` |
| `Could not resolve host: github.com` | Sem rede/DNS | Verifica ligação, proxy, VPN |

## Push / pull / merge

| Erro | Causa | Solução |
|---|---|---|
| `updates were rejected (fetch first)` | Remote avançou | `git pull` + resolve + `push` 🟢 |
| `no upstream branch` | Sem tracking | `git push -u origin <branch>` 🟢 |
| `Automatic merge failed` | Conflito | [[01-conflitos-e-recuperacao\|Resolver conflitos]] 🟢 |
| `Your local changes would be overwritten` | Working tree suja | `stash` / `commit` antes de trocar 🟢 |
| `failed to push to protected branch` | Proteção | Abrir PR 🟢 |

## Commits e histórico

| Erro | Causa | Solução |
|---|---|---|
| `nothing to commit` | Nada staged | `git add` 🟢 |
| `Author identity unknown` | Sem identidade | [[01-Instalacao-e-configuracao-inicial#2-configuração-mínima-obrigatória\|Configurar identidade]] 🟢 |
| Commit na branch errada (sem push) | Distração | `git reset --soft HEAD~1` + `stash`/`switch` + recommit 🟡 |
| Commit na branch errada (com push) | Distração | `git revert` no sítio errado + `cherry-pick` para o certo 🟡 |
| `lost` commits após reset/-D | Reescrita | `git reflog` + recupera 🟢 ([[01-reset-revert-reflog\|guia]]) |

## Diversos

| Erro | Causa | Solução |
|---|---|---|
| Ficheiro ignorado não entra | Regra `.gitignore` | `git check-ignore -v <f>`; `git add -f` só em exceção 🟡 |
| Tags não aparecem no GitHub | `push` não envia tags | `git push origin --tags` 🟢 |
| `detached HEAD` | Checkout de commit/hash | `git switch -c novo-branch` ou volta a um branch 🟢 |
| Repo aninhado (Git dentro de Git) | `init`/`clone` na pasta errada | Apaga `.git` interno **só** se for o errado 🔴 (confirma `git rev-parse --show-toplevel` primeiro) |

> [!CAUTION]
> Antes de qualquer comando 🟡/🔴: `git status` + `git stash list` + confirma o branch (`git branch --show-current`).
