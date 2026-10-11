# 07 — .gitignore, stash, restore

> **Nível:** 🟢 → 🟡 · **Selo:** 🟢 Seguro (com uma exceção 🟡 assinalada)

## `.gitignore` 🟢

**Sintaxe:** ficheiro `.gitignore` na raiz (ou subpastas), um padrão por linha.
**O que faz:** impede que caminhos sejam tracked. **Só afeta ficheiros ainda untracked** — não remove do histórico quem já foi commitado.
**Quando usar:** desde o `git init`: dependências, builds, segredos, ficheiros do OS/IDE.

```gitignore
# Dependências e build
node_modules/
dist/
build/
*.log

# Segredos e ambiente
.env
.env.local
*.pem

# OS / IDE
.DS_Store
Thumbs.db
.vscode/
.idea/
```

```bash
git check-ignore -v .env   # confirma que regra ignora o ficheiro
git rm --cached .env       # 🟡 deixa de seguir um ficheiro já commitado (mantém no disco)
```

> [!WARNING]
> `.gitignore` **não apaga segredos do histórico**. Se commitastes um `.env`, ver [[01-conflitos-e-recuperacao#5-segredos-no-histórico|recuperação]] e roda as credenciais.

## `git stash` 🟢 (uso normal)

**Sintaxe:** `git stash [push -m "msg"] [--include-untracked] | list | apply | pop | drop`
**O que faz:** guarda working tree + staging numa pilha temporária e limpa o diretório. Ideal para trocar de branch com trabalho a meio.
**Quando usar:** interromper tarefa sem commitar lixo.

```bash
git stash push -m "wip: formulario a meio"   # guarda
git stash list                               # vê a pilha
git switch outra-branch && git switch -      # trabalha noutro lado...
git stash pop                                # recupera e remove da pilha
```

| Comando | Efeito |
|---|---|
| `git stash push -m` | Guarda com nome |
| `git stash push -u` | Inclui ficheiros untracked (por omissão ficam!) |
| `git stash apply` | Recupera **mantendo** na pilha |
| `git stash pop` | Recupera **removendo** da pilha |
| `git stash drop` | 🟡 Apaga o stash (perde os dados!) |

## `git restore` 🟢 / 🟡

**Sintaxe (Git ≥ 2.23):** `git restore [--staged] [--source=<commit>] [--] <caminho>`
**O que faz:** repõe ficheiros. Seguro para unstaging; **descarta edições** quando toca na working tree.

```bash
git restore --staged app.js      # 🟢 tira do staging, mantém edições no disco
git restore app.js               # 🟡 descarta edições NÃO staged de app.js (perde trabalho!)
git restore --source=HEAD~2 app.js  # repõe versão de 2 commits atrás
```

**Alternativas e diferenças:**

| Objetivo | Moderno | Clássico (ainda válido) |
|---|---|---|
| Tirar do staging | `git restore --staged` | `git reset HEAD <ficheiro>` |
| Descartar edições | `git restore <ficheiro>` | `git checkout -- <ficheiro>` |
| Mudar de branch | `git switch` | `git checkout <branch>` |

> [!TIP]
> Prefere `switch`/`restore` (comandos com uma função cada) a `checkout` (faz tudo, mais fácil errar). Ver [[01-branches-switch-checkout|Branches]].

## Critérios de conclusão
- [ ] Tens `.gitignore` funcional desde o início de um repo de teste.
- [ ] Guardas e recuperas trabalho a meio com `stash push/pop`.

**Próximo:** [[01-branches-switch-checkout|Branches]]
