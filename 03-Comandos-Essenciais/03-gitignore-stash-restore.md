# 07 — .gitignore, stash, restore

> **Nível:** Iniciante para Intermédio · **Pré-requisito:** [[01-init-clone-status-add-commit|05 — init/clone/status/add/commit]] · **Tempo estimado:** 60 min
> **Objetivo:** ignorar o que não deve ser versionado, guardar trabalho a meio sem commits lixo e desfazer com o comando certo para cada caso.

## 1. Visão geral: três formas de "não commitar agora"

| Preciso de... | Ferramenta | Efeito |
|---|---|---|
| Nunca versionar (deps, builds, segredos) | `.gitignore` | Git finge que não vê |
| Guardar trabalho a meio e limpar o disco | `git stash` | Pilha temporária recuperável |
| Anular staging ou edições | `git restore` | Repõe a partir do histórico/índice |

---

### Conceito: `.gitignore`

**Selo:** [SEGURO]
**Definição:** ficheiro de padrões (um por linha) que impede caminhos de serem seguidos pelo Git.
**Quando utilizar:** desde o `git init`: dependências, builds, segredos, ficheiros do OS/IDE.
**Funcionamento:** só afeta ficheiros ainda **untracked** — não remove do histórico quem já foi commitado, nem apaga segredos antigos.

```gitignore
# Dependências e build
node_modules/
dist/
build/
*.log

# Segredos e ambiente (nunca versionar)
.env
.env.local
*.pem

# OS / IDE
.DS_Store
Thumbs.db
.vscode/
.idea/
```

**Demonstração linha por linha:**

```bash
echo ".env" >> .gitignore          # 1. declara a regra
git check-ignore -v .env           # 2. confirma que regra ignora o ficheiro (mostra ficheiro:linha:padrão)
git add .gitignore                 # 3. o próprio .gitignore DEVE ser commitado
git rm --cached .env               # 4. [ATENCAO] deixa de seguir ficheiro já commitado, mantendo-o no disco
```

> [!WARNING]
> `.gitignore` **não apaga segredos do histórico**. Se commitastes um `.env`, roda as credenciais primeiro e segue a [[01-conflitos-e-recuperacao#5-recuperacao-de-desastres|recuperação de desastres]].
> **Regra de memória:** "gitignore = porteiro: barra quem ainda não entrou, mas não expulsa quem já está dentro."

**Erro frequente e correção:** "adicionei ao `.gitignore` mas o Git continua a seguir" → o ficheiro já era tracked; corrige com `git rm --cached <ficheiro>`.

---

### Comando: `git stash`

**Selo:** [SEGURO] (uso normal; `drop` é [ATENCAO])
**Definição:** guarda working tree + staging numa pilha temporária e limpa o diretório.
**Quando utilizar:** interromper uma tarefa a meio para trocar de branch, puxar atualizações ou testar algo — sem commitar lixo.
**Sintaxe:** `git stash [push -m "msg"] [--include-untracked] | list | apply | pop | drop`
**O que significa cada parte:** `push -m` guarda com nome; `-u/--include-untracked` inclui ficheiros novos (por omissão ficam no disco!); `apply` recupera mantendo na pilha; `pop` recupera removendo; `drop` apaga ([ATENCAO]).

**Demonstração linha por linha:**

```bash
git stash push -m "wip: formulario a meio"   # guarda e limpa o disco
git stash list                               # vê a pilha (stash@{0}, ...)
git switch outra-branch && git switch -      # trabalha noutro lado...
git stash pop                                # recupera e remove da pilha
git stash list                               # confirma que saiu da pilha
```

| Comando | Efeito | Risco |
|---|---|---|
| `git stash push -m "msg"` | Guarda com nome | [SEGURO] |
| `git stash push -u` | Inclui untracked | [SEGURO] |
| `git stash apply` | Recupera mantendo na pilha | [SEGURO] |
| `git stash pop` | Recupera removendo da pilha | [SEGURO] |
| `git stash drop` | Apaga o stash | [ATENCAO] — perde os dados |

**Antes / depois:** antes do `push`, disco sujo; depois, disco limpo e pilha com 1 entrada. `pop` inverte.
**Regra de memória:** "stash = gaveta temporária com etiqueta; pop esvazia a gaveta."

---

### Comando: `git restore`

**Selo:** [SEGURO] para `--staged`; [ATENCAO] quando toca na working tree (descarta edições)
**Definição:** repõe ficheiros a partir do índice ou de um commit.
**Quando utilizar:** tirar algo do staging (seguro) ou descartar edições do disco (perigoso — confirma `status`/`diff` antes).
**Sintaxe (Git ≥ 2.23):** `git restore [--staged] [--source=<commit>] [--] <caminho>`

```bash
git restore --staged app.js                     # [SEGURO] tira do staging, mantém edições no disco
git diff app.js                                 # confirma o que vais descartar antes!
git restore app.js                              # [ATENCAO] descarta edições NÃO staged (perde trabalho)
git restore --source=HEAD~2 app.js              # repõe a versão de 2 commits atrás
```

**Alternativas e diferenças:**

| Objetivo | Moderno (recomendado) | Clássico (ainda válido) |
|---|---|---|
| Tirar do staging | `git restore --staged` | `git reset HEAD <ficheiro>` |
| Descartar edições | `git restore <ficheiro>` | `git checkout -- <ficheiro>` |
| Mudar de branch | `git switch` | `git checkout <branch>` |

> [!TIP]
> Prefere `switch`/`restore` (um comando, uma função) a `checkout` (faz tudo — mais fácil errar). Ver [[01-branches-switch-checkout|08 — Branches]].

**Regra de memória:** "restore com --staged mexe na mala; sem flag mexe no disco — e o disco não tem undo."

## 2. Prática guiada

1. Cria `.gitignore` com `*.log` e `.env` mas permite `exemplo.env` (dica: negação com `!`); confirma com `git check-ignore -v`.
2. A meio de uma edição, faz `stash push -m`, troca de branch, volta e faz `pop` — zero perdas.
3. Prepara um ficheiro, tira-o do staging com `restore --staged` e confirma que o conteúdo no disco sobreviveu.

## 3. Avaliação

**Perguntas de compreensão:**

1. `.gitignore` remove um ficheiro do histórico? O que é preciso para deixar de o seguir?
2. Qual a diferença entre `stash apply` e `stash pop`? Quando preferes cada um?
3. Porque `git restore app.js` exige mais cuidado que `git restore --staged app.js`?

**Exercício prático:** simula interrupção real: edição a meio → stash → cria e testa outro branch → volta → pop → commit final limpo.

**Desafio de interpretação:** `git stash push` guardou mas um ficheiro novo `rascunho.txt` ficou no disco. Porquê e como o incluirias? (Resposta: por omissão stash ignora untracked; usar `-u`.)

**Resumo visual:**

| Preciso de... | Comando |
|---|---|
| Ignorar caminho | regra no `.gitignore` + `git check-ignore -v` |
| Parar de seguir (mantém disco) | `git rm --cached <f>` |
| Guardar trabalho a meio | `git stash push -m "wip"` / `pop` |
| Tirar do staging | `git restore --staged <f>` |
| Descartar edições [ATENCAO] | `git restore <f>` (depois de `diff`) |

**Checklist de domínio:**

- [ ] Tens `.gitignore` funcional desde o início de um repo de teste.
- [ ] Guardas e recuperas trabalho a meio com `stash push/pop`.
- [ ] Distingues `restore --staged` de `restore` e sabes verificar antes do segundo.

**Próximo:** [[01-branches-switch-checkout|08 — Branches]]
