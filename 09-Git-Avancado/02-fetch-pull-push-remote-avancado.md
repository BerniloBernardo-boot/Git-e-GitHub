# 17 — fetch, pull, push e remote (avançado)

> **Nível:** 🟠 Avançado · **Pré-requisito:** [[01-repositorios-remotes-tags|Repositórios e remotes]]

## 1. Refspec e tracking (como o Git mapeia branches)

- Branch local `feature-x` com **upstream** `origin/feature-x`: `git push`/`pull` sem argumentos sabem o que fazer.
- Ver: `git branch -vv`. Definir: `git push -u origin feature-x` ou `git branch --set-upstream-to=origin/main`.

```bash
git branch -vv
# * feature-x  a1b2c3 [origin/feature-x: ahead 2] feat: ...
git branch --set-upstream-to=origin/develop
```

## 2. `git fetch` avançado 🟢

```bash
git fetch origin                          # tudo
git fetch origin develop                  # só um branch
git fetch --prune origin                  # 🟢 limpa refs de branches apagados no remote
git fetch --prune --all
git log --oneline main..origin/main       # o que chegou?
git diff main...origin/main               # diff de 3 pontos (desde a base comum)
```

> [!TIP]
> Configura prune automático: `git config --global fetch.prune true`. Evita lista de branches-fantasma.

## 3. `git pull` avançado 🟢/🟡

`git pull` = `fetch` + integração. Controla a 2ª fase:

```bash
git pull --rebase          # linear (ideal em feature privada, sem push feito)
git pull --ff-only         # só atualiza se for fast-forward; falha se divergiu (o mais seguro p/ main/develop)
git config --global pull.ff only   # torna ff-only o comportamento padrão
```

| Estratégia | Config | Efeito |
|---|---|---|
| merge (omissão clássica) | `pull.rebase false` | Cria merge commit se divergir |
| rebase | `pull.rebase true` | Reaplica os teus commits por cima |
| só fast-forward | `pull.ff only` | Falha em vez de criar merge — tu decides depois |

## 4. `git push` avançado 🟢/🟡

```bash
git push origin HEAD:refs/heads/feature-x   # forma explícita (src:dst)
git push --force-with-lease                 # 🟡 reescreve SÓ se ninguém avançou desde o teu fetch
git push --delete origin feature-velha      # apaga branch remoto
git push origin --tags                      # publica tags
```

> [!CAUTION]
> **Nunca `push --force` bruto em branches partilhados** — apaga commits de colegas silenciosamente. `--force-with-lease` aborta se o remote avançou. Em `main`/`develop` protegidos, o force é bloqueado pelo GitHub.

## 5. Trabalhar com forks (upstream) 🟢

```bash
git remote add upstream git@github.com:ORIGINAL/repo.git
git fetch upstream
git switch -c minha-feature upstream/main
# ... trabalha ...
git push -u origin minha-feature   # PR do teu fork para o original
git fetch upstream && git merge upstream/main   # manter sincronizado
```

## Critérios de conclusão
- [ ] Configuras `fetch.prune` e `pull.ff only` e explicas porquê.
- [ ] Sincronizas um fork com `upstream` sem ajuda.

**Relacionadas:** [[01-repositorios-remotes-tags|Remotes (base)]] · [[02-merge-rebase-cherry-pick|merge vs. rebase]]
