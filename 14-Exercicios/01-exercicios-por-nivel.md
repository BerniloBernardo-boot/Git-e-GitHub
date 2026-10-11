# 23 — Exercícios por nível

> Faz por ordem. Cada nível tem **critério de conclusão** — só avança quando cumprires todos.

## 🟢 Iniciante (módulos 01–03)

- [ ] E1. `init` + 3 commits + `log --oneline`. Critério: explicas cada hash.
- [ ] E2. Prevê `git status --short` antes de correr (10 rondas). Critério: ≥ 8 acertos.
- [ ] E3. `.gitignore` que ignora `*.log` e `.env` mas permite `exemplo.env`. Critério: `git check-ignore` confirma.
- [ ] E4. `stash` a meio de tarefa, troca de branch, `pop`. Critério: zero perdas.

## 🟡 Intermédio (módulos 04–07)

- [ ] E5. Feature branch + `merge --no-ff` em `main` local. Critério: grafo mostra merge commit.
- [ ] E6. Publica repo no GitHub com SSH, protege `main`. Critério: push direto recusado.
- [ ] E7. PR com `Closes #N`, CI (lint) verde, review de colega, squash merge. Critério: issue fechou sozinha.
- [ ] E8. Provoca conflito (mesma linha em 2 branches) e resolve. Critério: `git diff --check` limpo + testes passam.

## 🟠 Avançado (módulos 08–09)

- [ ] E9. Atualiza feature com `rebase` + `push --force-with-lease`. Critério: histórico linear, sem queixas.
- [ ] E10. Commit errado com push → `revert`. Commit local mau → `reset --soft`. Critério: justificas cada escolha.
- [ ] E11. Apaga branch com `-D` e recupera via `reflog`. Critério: recuperado em < 5 min.
- [ ] E12. Fork + `upstream`, PR para o original. Critério: PR merged.

## 🔴 Profissional (módulos 10–11)

- [ ] E13. Reescreve 5 mensagens para Conventional Commits; tag `v1.0.0`; release com notas. Critério: changelog gerado faz sentido.
- [ ] E14. Sprint simulada do [[02-Workflow-Cuidar-Angola|Cuidar Angola]] (issues → PRs → release). Critério: equipa avalia o processo.
- [ ] E15. Secret scanning (`gitleaks`) limpo + assinatura GPG ativa. Critério: commits "Verified".

**Projetos guiados:** [[01-projetos-progressivos|Projetos práticos]]
