# 19 — Segurança e boas práticas profissionais

> **Nível:** 🔴 Profissional

## 1. Segredos: prevenção

- [ ] `.env`, `*.pem`, `*.key`, credenciais **no `.gitignore` desde o `init`**.
- [ ] Segredos de CI só em **Actions Secrets**; acesso por `${{ secrets.NOME }}`.
- [ ] Tokens com **âmbito mínimo** e validade curta; 1 token por uso.
- [ ] Revisão de PR verifica diffs por segredos (`git diff --staged` antes de commitar).
- [ ] Ferramentas: `gitleaks`, GitHub secret scanning / push protection.

## 2. Segredo vazou — e agora?

1. **Roda/revoga a credencial no serviço primeiro** (o histórico pode ser copiado por qualquer clone).
2. Remove do código: `git rm --cached .env` + commit.
3. Limpa o histórico **se preciso** com `git filter-repo` (reescrita — coordena a equipa: todos re-clonam; ver [[01-reset-revert-reflog|reescrita]]).
4. Força push em branches afetados (**só** com acordo da equipa) e avisa.

> [!CAUTION]
> Apagar o ficheiro num commit novo **não chega**: o segredo continua em commits antigos. Assume-o como comprometido até rodado.

## 3. Assinatura de commits (opcional, recomendado)

```bash
gpg --full-generate-key          # cria chave GPG
git config --global user.signingkey <ID>
git config --global commit.gpgsign true
git log --show-signature -1      # verifica
```

No GitHub: regista a chave pública em Settings → SSH and GPG keys → selo "Verified" nos commits.

## 4. Boas práticas de equipa (checklist)

- [ ] `main`/`develop` protegidos; tudo por PR com review + CI.
- [ ] PRs pequenos e focados; template de PR.
- [ ] [[01-conventional-commits-semver-cicd|Conventional Commits]] + SemVer + releases com notas.
- [ ] `git pull --ff-only` em `main`/`develop`; `fetch.prune true`.
- [ ] Nunca `--force` em partilhados; `--force-with-lease` só em feature privada e combinado.
- [ ] `git status` antes de cada operação; `add` seletivo (nunca `add .` cego).
- [ ] Documenta decisões no PR, não só no chat.

## Critérios de conclusão
- [ ] Um repo teu passa num scan de segredos e tem branches protegidos.
- [ ] Explicas o plano de resposta a vazamento de segredo.

**Relacionadas:** [[02-SSH-e-autenticacao|Autenticação]] · [[02-Workflow-Cuidar-Angola|Cuidar Angola]]
