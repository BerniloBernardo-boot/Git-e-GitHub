# 19 — Segurança e boas práticas profissionais

> **Nível:** Profissional · **Pré-requisitos:** [[02-SSH-e-autenticacao|04]], [[01-conventional-commits-semver-cicd|18]] · **Tempo estimado:** 60 min
> **Objetivo:** prevenir vazamento de segredos, responder corretamente se vazar e manter higiene de equipa auditável.

## 1. Definição e finalidade

> **Definição:** segurança no Git = impedir que segredos entrem no histórico + garantir que integrações passam por review e CI + saber responder quando algo vaza.

**Finalidade:** um segredo commitado espalha-se por cada clone e fica no histórico para sempre — apagar o ficheiro depois não chega. Prevenção barata supera remediação cara.

## 2. Segredos: prevenção (checklist)

- [ ] `.env`, `*.pem`, `*.key`, credenciais **no `.gitignore` desde o `init`** (ver lição [[03-gitignore-stash-restore|07]]).
- [ ] Segredos de CI só em **Actions Secrets**; acesso por `${{ secrets.NOME }}`.
- [ ] Tokens com **âmbito mínimo** e validade curta; 1 token por uso.
- [ ] Revê `git diff --staged` antes de cada commit à procura de segredos.
- [ ] Ferramentas: `gitleaks`, GitHub secret scanning / push protection.

```bash
# Verificação antes de cada commit (hábito):
git diff --staged --stat   # que ficheiros vão?
git diff --staged | grep -iE "token|secret|password|api[_-]?key" || echo "sem matches óbvios"
```

## 3. Segredo vazou — e agora? (ordem importa)

1. **Roda/revoga a credencial no serviço primeiro** (o histórico pode ser copiado por qualquer clone — apagar depois não descompromete).
2. Remove do código: `git rm --cached .env` + commit.
3. Limpa o histórico **se preciso** com `git filter-repo` ([DESTRUTIVO] — reescrita; coordena a equipa: todos re-clonam; ver [[01-reset-revert-reflog|16]]).
4. Push nos branches afetados (**só** com acordo da equipa) e avisa pelos canais oficiais.

> [!CAUTION]
> Apagar o ficheiro num commit novo **não chega**: o segredo continua em commits antigos. Assume-o como comprometido até rodado.

**Regra de memória:** "Vazou? Roda primeiro, limpa depois, avisa sempre."

## 4. Assinatura de commits (opcional, recomendado)

> **Definição:** assinatura GPG/SSH prova autoria — selo "Verified" no GitHub.

```bash
gpg --full-generate-key          # 1. cria chave GPG
git config --global user.signingkey <ID>   # 2. regista-a no Git
git config --global commit.gpgsign true    # 3. assina por omissão
git log --show-signature -1                # 4. verifica
```

No GitHub: regista a chave pública em Settings → SSH and GPG keys → selo "Verified" nos commits.

## 5. Boas práticas de equipa (checklist)

- [ ] `main`/`develop` protegidos; tudo por PR com review + CI.
- [ ] PRs pequenos e focados; template de PR (lição [[01-pull-requests-e-code-review|12]]).
- [ ] [[01-conventional-commits-semver-cicd|Conventional Commits]] + SemVer + releases com notas.
- [ ] `git pull --ff-only` em `main`/`develop`; `fetch.prune true`.
- [ ] Nunca `--force` em partilhados; `--force-with-lease` só em feature privada e combinado.
- [ ] `git status` antes de cada operação; `add` seletivo (nunca `add .` cego).
- [ ] Documenta decisões no PR, não só no chat.

## 6. Prática guiada

1. Corre um scan (`gitleaks detect --source .` ou secret scanning do GitHub) num repo teu e interpreta o relatório.
2. Simula vazamento num repo descartável: commita `.env` falso, executa o plano da secção 3.
3. Ativa assinatura e obtém "Verified" num commit de teste.

## 7. Avaliação

**Perguntas de compreensão:**

1. Porque apagar o segredo num commit novo não resolve? Qual o primeiro passo correto?
2. O que `git filter-repo` faz e porque exige coordenação da equipa?
3. Para que serve a assinatura de commits?

**Exercício prático:** repo de teste com scan limpo, branches protegidos e commit assinado "Verified".

**Desafio de interpretação:** colega fez push de `.env` real há 10 minutos e já há 3 clones. Lista a ordem de ações. (Resposta: 1. rodar a credencial no serviço; 2. `rm --cached` + commit; 3. avaliar reescrita com equipa; 4. avisar.)

**Resumo visual:**

| Fase | Ação |
|---|---|
| Prevenir | `.gitignore` desde o init + `diff --staged` + scan |
| Vazar | rodar credencial → remover → reescrever (coordenado) → avisar |
| Provar autoria | assinatura GPG/SSH → "Verified" |
| Higiene | branches protegidos + PR + CI + convenções |

**Checklist de domínio:**

- [ ] Um repo teu passa num scan de segredos e tem branches protegidos.
- [ ] Explicas o plano de resposta a vazamento pela ordem correta.
- [ ] Praticas `status` + `diff --staged` antes de cada commit.

**Relacionadas:** [[02-SSH-e-autenticacao|04 — Autenticação]] · [[02-Workflow-Cuidar-Angola|15 — Cuidar Angola]]
