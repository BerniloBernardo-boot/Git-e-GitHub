# 03 — Instalação e configuração inicial

> **Nível:** 🟢 Iniciante · **Selo:** 🟢 Seguro

## 1. Instalação

| Sistema | Comando |
|---|---|
| Debian/Ubuntu | `sudo apt update && sudo apt install git` |
| Fedora | `sudo dnf install git` |
| Arch | `sudo pacman -S git` |
| macOS | `brew install git` (ou Xcode Command Line Tools) |
| Windows | Instalador em `git-scm.com` (inclui Git Bash) |

Verificar:

```bash
git --version
# Resultado esperado: git version 2.x.x
```

## 2. Configuração mínima obrigatória

```bash
git config --global user.name "O Teu Nome"
git config --global user.email "teu@email.com"
git config --global init.defaultBranch main
git config --global pull.rebase false   # merge por omissão no pull (menos surpresas p/ iniciantes)
git config --global core.editor "code --wait"  # ou nano, vim
```

**O que faz:** grava identidade usada em todos os commits. Sem `user.name`/`user.email`, o `git commit` falha com erro a pedir a configuração.

**Ver configuração:**

```bash
git config --global --list
git config user.name   # lê valor efetivo (local sobrepõe-se ao global)
```

> [!TIP]
> Para usar email diferente no trabalho vs. projetos pessoais, define `user.email` **local** dentro de cada repo: `git config user.email "profissional@empresa.com"` (sem `--global`).

## 3. Configurações recomendadas (nível profissional)

```bash
# Atalhos
git config --global alias.st "status --short"
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.lg "log --oneline --graph --decorate -15"

# Cores e diffs legíveis
git config --global color.ui auto

# Evita Rebase forçado acidental e ensina o push simples
git config --global push.default simple
```

## 4. Erros frequentes

| Erro | Causa | Solução |
|---|---|---|
| `Author identity unknown` no commit | Falta `user.name`/`user.email` | Executa os dois `git config --global` acima |
| Editor estranho abre no commit | `core.editor` não definido | Define `core.editor` ou usa `git commit -m` |
| Branch inicial `master` em vez de `main` | Git antigo (< 2.28) | `git init -b main` ou `init.defaultBranch main` |

## Critérios de conclusão
- [ ] `git --version` funciona e identidade global está definida.
- [ ] Sabes ver e sobrepor configuração local vs. global.

**Próximo:** [[02-SSH-e-autenticacao|SSH e autenticação]] · **Início:** [[README|Índice do guia]]
