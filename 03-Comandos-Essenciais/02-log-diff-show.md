# 06 — log, diff, show

> **Nível:** 🟢 Iniciante · **Selo:** 🟢 Seguro (todos só leem)

## `git log` 🟢

**Sintaxe:** `git log [--oneline] [--graph --decorate] [-n] [-- <caminho>]`
**O que faz:** lista commits do HEAD para trás. **Quando usar:** auditar histórico, encontrar hashes, preparar `revert`/`reset`.

```bash
git log --oneline -5
# a1b2c3d feat: adiciona validacao do login
# 9f8e7d6 fix: corrige typo no README
# ...

git log --oneline --graph --decorate -10   # histórico com branches/tags
git log -- app.js                          # só commits que tocaram app.js
git log -S "validarEmail"                  # pickaxe: onde aparece/desaparece um texto
```

## `git diff` 🟢

**Sintaxe:** `git diff [--staged] [<commit> [<commit>]] [-- <caminho>]`
**O que faz:** mostra diferenças entre zonas. A distinção mais importante do Git:

| Comando | Compara |
|---|---|
| `git diff` | working tree vs. staging (o que **ainda não** foi `add`) |
| `git diff --staged` | staging vs. último commit (o que **vai** no próximo commit) |
| `git diff main..feature` | dois commits/branches |
| `git diff HEAD` | working tree + staging vs. último commit |

```bash
echo "nova linha" >> app.txt
git diff            # mostra a linha adicionada (ainda não staged)
git add app.txt
git diff            # vazio agora!
git diff --staged   # mostra a linha (vai no commit)
```

## `git show` 🟢

**Sintaxe:** `git show [<commit>] [--stat] [-- <caminho>]`
**O que faz:** mostra metadados + diff de um commit (por omissão, o HEAD).

```bash
git show --stat HEAD
# commit a1b2c3d... | Author: ... | Date: ...
#  login.js | 20 +++++++++++++++-----
#  1 file changed, 15 insertions(+), 5 deletions(-)

git show 9f8e7d6 -- README.md   # diff daquele commit só no README
```

## Dicas profissionais

- `git log --oneline --graph --decorate --all -20` → mapa completo dos branches.
- No Windows (cmd), aspas e paginação (`less`) comportam-se diferente; `git --no-pager log -5` evita o pager.
- Alias útil: `git config --global alias.lg "log --oneline --graph --decorate -15"`.

## Critérios de conclusão
- [ ] Explicas a diferença `git diff` vs. `git diff --staged` com um exemplo.
- [ ] Encontras o commit que introduziu uma linha usando `git log -S`.

**Próximo:** [[03-gitignore-stash-restore|.gitignore, stash, restore]]
