# 03 — Instalação e configuração inicial

> **Nível:** Iniciante · **Pré-requisitos:** nenhum · **Tempo estimado:** 30 min
> **Objetivo:** ter o Git funcional com identidade definida e atalhos que aceleram o estudo.

## 1. Definição e finalidade

> **Definição:** instalar o Git e configurar identidade (`user.name`, `user.email`) e preferências (branch padrão, editor, aliases).

**Finalidade:** sem identidade, `git commit` falha; sem branch padrão `main`, cada `init` cria o nome herdado `master`; sem editor definido, o Git abre um editor desconhecido. Cinco minutos aqui poupam horas de erros.

## 2. Instalação (por sistema)

| Sistema | Comando |
|---|---|
| Debian/Ubuntu | `sudo apt update && sudo apt install git` |
| Fedora | `sudo dnf install git` |
| Arch | `sudo pacman -S git` |
| macOS | `brew install git` (ou Xcode Command Line Tools) |
| Windows | Instalador em `git-scm.com` (inclui Git Bash) |

**Verificação:**

```bash
git --version   # esperado (exemplo simulado): "git version 2.45.0"
```

Se o comando não for encontrado no Windows, usa o **Git Bash** instalado com o Git.

## 3. Configuração mínima obrigatória

> **Definição:** `git config` grava pares chave-valor em três níveis: `--system` (toda a máquina), `--global` (o teu utilizador, `~/.gitconfig`) e local (o repo atual, `.git/config`). O nível local sobrepõe-se ao global.

```bash
git config --global user.name "O Teu Nome"             # autor dos commits
git config --global user.email "teu@email.com"         # email dos commits
git config --global init.defaultBranch main            # novos repos nascem em "main"
git config --global pull.rebase false                  # pull faz merge por omissão (menos surpresas no início)
git config --global core.editor "code --wait"          # ou nano, vim
```

Linha a linha: as duas primeiras definem a **identidade** usada em cada commit; a terceira evita o branch `master`; a quarta mantém o comportamento de `pull` previsível para iniciantes; a quinta escolhe o editor das mensagens de commit.

**Verificação:**

```bash
git config --global --list   # mostra toda a config global
git config user.name         # lê o valor efetivo (local sobrepõe-se ao global)
```

> [!TIP]
> Email diferente no trabalho vs. projetos pessoais? Define `user.email` **local** dentro de cada repo: `git config user.email "profissional@empresa.com"` (sem `--global`).

**Antes / depois:**

| | Antes | Depois |
|---|---|---|
| `git commit` | Falha com `Author identity unknown` | Funciona |
| `git init` | Cria branch `master` (Git antigo) | Cria `main` |
| `git commit` sem `-m` | Abre editor desconhecido | Abre o editor configurado |

## 4. Configurações recomendadas (nível profissional)

```bash
# Atalhos (menos digitação, menos erros)
git config --global alias.st "status --short"
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --decorate -15"

# Cores e push simples e seguro
git config --global color.ui auto
git config --global push.default simple
```

**Regra de memória:** "Configura uma vez, usa para sempre: quem sou, onde começa, como edita."

## 5. Erros frequentes

| Erro | Causa | Solução |
|---|---|---|
| `Author identity unknown` no commit | Falta `user.name`/`user.email` | Executa os dois `git config --global` acima |
| Editor estranho abre no commit | `core.editor` não definido | Define `core.editor` ou usa sempre `git commit -m` |
| Branch inicial `master` em vez de `main` | Git antigo (< 2.28) | `git init -b main` ou `init.defaultBranch main` |

## 6. Prática guiada

1. Corre `git --version` e regista a versão.
2. Define nome, email e branch padrão; confirma com `git config --global --list`.
3. Cria um repo de teste e define um email local diferente; confirma com `git config user.email` dentro e fora do repo.

## 7. Avaliação

**Perguntas de compreensão:**

1. Para que servem `user.name` e `user.email`? Onde ficam gravados com `--global`?
2. Que nível de configuração ganha quando há conflito: local ou global? Como verificas o valor efetivo?
3. Porque definir `init.defaultBranch main`?

**Exercício prático:** configura os 4 aliases acima e demonstra `git st` e `git lg` num repo de teste.

**Desafio de interpretação:** `git config user.email` mostra `a@x.com` mas `git config --global user.email` mostra `b@y.com`. Qual vai no próximo commit? (Resposta: `a@x.com` — o local sobrepõe-se.)

**Resumo visual:**

| Preciso de... | Comando |
|---|---|
| Ver versão | `git --version` |
| Definir identidade | `git config --global user.name/email` |
| Ver config efetiva | `git config --list` / `git config <chave>` |
| Atalhos | `git config --global alias.<x> "<comando>"` |

**Checklist de domínio:**

- [ ] `git --version` funciona e a identidade global está definida.
- [ ] Sabes ver e sobrepor configuração local vs. global.
- [ ] Aliases `st` e `lg` funcionam.

**Próximo:** [[02-SSH-e-autenticacao|04 — SSH e autenticação]] · **Início:** [[README|Índice do guia]]
