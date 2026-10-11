# 04 — SSH e autenticação no GitHub

> **Nível:** Iniciante para Intermédio · **Pré-requisito:** [[01-Instalacao-e-configuracao-inicial|03 — Instalação e configuração]] · **Tempo estimado:** 45 min
> **Objetivo:** clonar, puxar e publicar via SSH ou HTTPS+token, e diagnosticar os 4 erros mais comuns.

## 1. Definição e finalidade

> **Definição:** autenticação prova ao GitHub quem és quando fazes `clone`, `fetch`, `pull` ou `push` pela rede.

**Finalidade:** sem ela, consegues trabalhar localmente mas não trocar código com o remoto. O GitHub deixou de aceitar password no HTTPS em 2021 — restam chaves SSH, tokens (PAT) ou GitHub CLI.

## 2. As 3 formas de autenticar (comparação)

| Método | Quando usar | Notas |
|---|---|---|
| **SSH** (recomendado no Linux, uso diário) | Clonar/push sem digitar credenciais | Par de chaves; a pública fica registada no GitHub |
| **HTTPS + Personal Access Token (PAT)** | Redes que bloqueiam SSH, uso ocasional | Usa o token como password; âmbito mínimo `repo` |
| **GitHub CLI (`gh`)** | Criar PRs/issues pelo terminal | Autenticação OAuth; prático para automação leve |

**Como funciona o SSH em 3 frases:** geras um par de chaves (privada fica na tua máquina, pública vai para o GitHub); o agente SSH desbloqueia a privada; o GitHub confirma que a privada corresponde à pública registada — sem passwords em cada operação.

## 3. SSH passo a passo (Linux)

```bash
# 1. Gerar chave (ed25519 é o standard atual)
ssh-keygen -t ed25519 -C "teu@email.com"
# Prime ENTER para aceitar ~/.ssh/id_ed25519; define passphrase (recomendado) ou deixa vazia

# 2. Iniciar o agente e adicionar a chave
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 3. Mostrar a chave pública para copiar para o GitHub
cat ~/.ssh/id_ed25519.pub
```

Regista no GitHub: **Settings → SSH and GPG keys → New SSH key** → colar o conteúdo do `.pub` (nunca o ficheiro sem `.pub` — esse é privado).

**Verificação:**

```bash
ssh -T git@github.com
# Esperado (exemplo simulado): "Hi <username>! You've successfully authenticated..."
```

**Clonar via SSH:**

```bash
git clone git@github.com:utilizador/repo.git
git remote -v   # confirma que origin usa o URL SSH
```

## 4. HTTPS + token

```bash
git clone https://github.com/utilizador/repo.git
# Username: o teu utilizador
# Password: cola um PAT (Settings → Developer settings → Personal access tokens)
```

> [!WARNING]
> Nunca guardes tokens em ficheiros versionados nem em screenshots. Se um token vazar, revoga-o imediatamente no GitHub. Ver [[02-seguranca-e-boas-praticas|19 — Segurança]].

Guardar credencial com segurança (Linux):

```bash
git config --global credential.helper store   # simples (ficheiro ~/.git-credentials)
# Alternativa mais segura: gestor do sistema (ex.: libsecret):
# git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```

**Antes / depois:**

| | Antes | Depois |
|---|---|---|
| `ssh -T git@github.com` | `Permission denied (publickey)` | Saudação com o teu username |
| `git push` via HTTPS | Pede credenciais sempre | Usa helper/token guardado |
| `git remote -v` | URL errado | URL SSH ou HTTPS correto e testado |

**Regra de memória:** "SSH = chave em casa, fechadura no GitHub; HTTPS = token como passe de acesso."

## 5. Erros frequentes

| Erro | Causa | Solução |
|---|---|---|
| `Permission denied (publickey)` | Chave não registada ou agente sem a chave | `ssh-add -l` para confirmar; regista a `.pub` no GitHub |
| `Host key verification failed` | `known_hosts` desatualizado | `ssh-keygen -R github.com` e volta a tentar |
| `Support for password authentication was removed` | Tentaste password no HTTPS | Usa PAT em vez da password |
| `Permission to user/repo denied` | Token sem âmbito `repo` ou SSH de outra conta | Verifica âmbitos do token / `ssh -T git@github.com` mostra a conta ativa |

## 6. Prática guiada

1. Gera a chave, regista-a e corre `ssh -T git@github.com` até veres a saudação.
2. Clona um repo teu via SSH e confirma `git remote -v`.
3. (Opcional) Configura um PAT com âmbito mínimo e testa um clone HTTPS numa pasta separada.

## 7. Avaliação

**Perguntas de compreensão:**

1. Que ficheiro vai para o GitHub: `id_ed25519` ou `id_ed25519.pub`? Porquê?
2. O GitHub aceita a tua password de login no `git push` via HTTPS? O que usar em vez disso?
3. `ssh -T` falhou com `Permission denied`. Lista duas causas e como as verificas.

**Exercício prático:** demonstra autenticação funcional (`ssh -T` com sucesso ou clone HTTPS com PAT) e explica quando escolherias cada método.

**Desafio de interpretação:** `git push` pede username/password mesmo já tendo SSH registado. O que isso sugere sobre o URL do remote? (Resposta: o remote usa URL HTTPS — confirma com `git remote -v`; para SSH, muda com `git remote set-url`.)

**Resumo visual:**

| Preciso de... | Comando |
|---|---|
| Gerar chave | `ssh-keygen -t ed25519 -C "email"` |
| Ativar chave | `eval "$(ssh-agent -s)" && ssh-add ~/.ssh/id_ed25519` |
| Testar | `ssh -T git@github.com` |
| Ver remote | `git remote -v` |

**Checklist de domínio:**

- [ ] `ssh -T git@github.com` autentica com sucesso **ou** clone HTTPS com PAT funciona.
- [ ] Sabes quando usar SSH vs. HTTPS+token.
- [ ] Nunca expuseste chave privada ou token.

**Relacionadas:** [[01-repositorios-remotes-tags|10 — Remotes]] · [[02-seguranca-e-boas-praticas|19 — Segurança]]
