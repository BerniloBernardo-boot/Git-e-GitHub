# 04 — SSH e autenticação no GitHub

> **Nível:** 🟢 Iniciante → 🟡 Intermédio · **Selo:** 🟢 Seguro

## 1. As 3 formas de autenticar

| Método | Quando usar | Notas |
|---|---|---|
| **SSH** (recomendado p/ uso diário no Linux) | Clonar/push sem digitar credenciais | Par de chaves; chave pública registada no GitHub |
| **HTTPS + Personal Access Token (PAT)** | Redes que bloqueiam SSH, uso ocasional | O GitHub **não aceita password** no HTTPS desde 2021 — usa token |
| **GitHub CLI (`gh`)** | Criar PRs/issues pelo terminal | Usa OAuth; prático |

## 2. SSH passo a passo (Linux)

```bash
# 1. Gerar chave (ed25519 é o standard atual)
ssh-keygen -t ed25519 -C "teu@email.com"
# Prime ENTER para aceitar ~/.ssh/id_ed25519 e definir (ou não) passphrase

# 2. Iniciar o agente e adicionar a chave
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 3. Mostrar a chave pública para copiar para o GitHub
cat ~/.ssh/id_ed25519.pub
```

Registar no GitHub: **Settings → SSH and GPG keys → New SSH key** → colar o conteúdo.

Testar:

```bash
ssh -T git@github.com
# Resultado esperado: "Hi <username>! You've successfully authenticated..."
```

Clonar via SSH:

```bash
git clone git@github.com:utilizador/repo.git
```

## 3. HTTPS + token

```bash
git clone https://github.com/utilizador/repo.git
# Username: o teu utilizador
# Password: cola um PAT (criado em Settings → Developer settings → Personal access tokens)
```

> [!WARNING]
> Nunca coles tokens em ficheiros versionados nem em screenshots. Se um token vazar, revoga-o imediatamente no GitHub. Ver [[02-seguranca-e-boas-praticas|Segurança]].

Guardar credencial com segurança (Linux):

```bash
git config --global credential.helper store   # simples (ficheiro ~/.git-credentials)
# Alternativa mais segura: usa o gestor do sistema (ex.: libsecret):
# git config --global credential.helper /usr/share/doc/git/contrib/credential/libsecret/git-credential-libsecret
```

## 4. Erros frequentes

| Erro | Causa | Solução |
|---|---|---|
| `Permission denied (publickey)` | Chave não registada ou agente sem a chave | `ssh-add -l` para confirmar; regista a `.pub` no GitHub |
| `Host key verification failed` | `known_hosts` desatualizado | `ssh-keygen -R github.com` e volta a tentar |
| `Support for password authentication was removed` | Tentaste password no HTTPS | Usa PAT em vez da password |
| `Permission to user/repo denied` | Token sem âmbito `repo` ou SSH de outra conta | Verifica âmbitos do token / `ssh -T git@github.com` mostra a conta ativa |

## Critérios de conclusão
- [ ] `ssh -T git@github.com` autentica com sucesso **ou** clone HTTPS com PAT funciona.
- [ ] Sabes quando usar SSH vs. HTTPS+token.

**Relacionadas:** [[01-repositorios-remotes-tags|Remotes]] · [[02-seguranca-e-boas-praticas|Segurança]]
