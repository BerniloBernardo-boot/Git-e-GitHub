# 21 — Erros comuns e soluções

> **Nível:** todos · **Uso:** consulta rápida por mensagem de erro.
> **Objetivo:** diagnosticar pela mensagem, aplicar a solução do risco certo e prevenir recorrência.
> **Regra de segurança:** antes de qualquer solução [ATENCAO]/[DESTRUTIVO]: `git status` + `git stash list` + `git branch --show-current`.

Legenda: [SEGURO] só lê ou soma · [ATENCAO] reescreve local · [DESTRUTIVO] pode apagar dados.

## Autenticação e ligação

| Erro | Causa | Solução |
|---|---|---|
| `Permission denied (publickey)` | SSH sem chave/autorização | [[02-SSH-e-autenticacao|04 — Configurar SSH]] [SEGURO] |
| `Support for password authentication was removed` | Password no HTTPS (descontinuada) | Usar PAT [SEGURO] |
| `repository not found` | URL errado / sem acesso | Confirma URL + acesso; `git remote -v` [SEGURO] |
| `Could not resolve host: github.com` | Sem rede/DNS | Verifica ligação, proxy, VPN |

## Push / pull / merge

| Erro | Causa | Solução |
|---|---|---|
| `updates were rejected (fetch first)` | Remote avançou | `git fetch` + integra + resolve + `push` [SEGURO] |
| `no upstream branch` | Sem tracking | `git push -u origin <branch>` [SEGURO] |
| `Automatic merge failed` | Conflito | [[01-conflitos-e-recuperacao|13 — Resolver conflitos]] [SEGURO] |
| `Your local changes would be overwritten` | Working tree suja | `stash` / `commit` antes de trocar [SEGURO] |
| `failed to push to protected branch` | Proteção | Abrir PR [SEGURO] |

## Commits e histórico

| Erro | Causa | Solução |
|---|---|---|
| `nothing to commit` | Nada staged | `git add` primeiro [SEGURO] |
| `Author identity unknown` | Sem identidade | [[01-Instalacao-e-configuracao-inicial|03 — Configurar identidade]] [SEGURO] |
| Commit na branch errada (sem push) | Distração | `git reset --soft HEAD~1` + `stash`/`switch` + recommit [ATENCAO] |
| Commit na branch errada (com push) | Distração | `git revert` no sítio errado + `cherry-pick` para o certo [ATENCAO] |
| Commits "perdidos" após reset/-D | Reescrita | `git reflog` + recupera ([[01-reset-revert-reflog|16]]) [SEGURO] |

## Diversos

| Erro | Causa | Solução |
|---|---|---|
| Ficheiro ignorado não entra | Regra `.gitignore` | `git check-ignore -v <f>`; `git add -f` só em exceção [ATENCAO] |
| Tags não aparecem no GitHub | `push` não envia tags | `git push origin --tags` [SEGURO] |
| `detached HEAD` | Checkout de commit/hash | `git switch -c novo-branch` ou volta a um branch [SEGURO] |
| Repo aninhado (Git dentro de Git) | `init`/`clone` na pasta errada | Apaga `.git` interno **só** se for o errado [DESTRUTIVO] (confirma `git rev-parse --show-toplevel` primeiro) |

## Como diagnosticar (método em 4 passos)

1. **Lê a mensagem toda** — o Git sugere quase sempre o comando (`hint:`).
2. **Localiza:** `git status --short`, `git branch --show-current`, `git log --oneline -3`, `git stash list`.
3. **Classifica o risco** da solução antes de correr (tabela acima).
4. **Verifica depois** com o mesmo `status`/`log` — o erro desapareceu e nada se perdeu?

## Avaliação

**Perguntas de compreensão:**

1. `updates were rejected`: o que significa e qual a sequência segura de resolução?
2. Commit na branch errada com push vs. sem push: porque soluções diferentes?
3. Que 3 comandos corres antes de qualquer solução [ATENCAO]/[DESTRUTIVO]?

**Exercício prático:** provoca 3 erros desta página num repo descartável e resolve-os documentando mensagem → causa → solução → verificação.

**Checklist de domínio:**

- [ ] Diagnosticas 10 erros desta página sem consultar a tabela.
- [ ] Nunca corres reescrita sem verificar `status` + branch atual.

> [!CAUTION]
> Comandos [DESTRUTIVO] (`reset --hard`, `branch -D`, `push --force`, `filter-repo`, apagar `.git`): confirma caminho, branch e stashes antes. Em dúvida, faz backup do repo (`cp -r`) ou `stash push` primeiro.
