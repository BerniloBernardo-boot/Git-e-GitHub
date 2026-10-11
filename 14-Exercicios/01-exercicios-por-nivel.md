# 23 — Exercícios por nível

> **Nível:** todos · **Uso:** faz por ordem. Cada nível tem critério de conclusão — só avança quando cumprires todos.
> **Método:** tenta sem consultar a solução; usa as pistas progressivas; confirma com os comandos de verificação indicados.

## Iniciante (módulos 01–03)

- [ ] **E1.** `init` + 3 commits + `log --oneline`. *Verificação:* explicas cada hash e mensagem. ([[01-init-clone-status-add-commit|05]])
- [ ] **E2.** Prevê `git status --short` antes de correr (10 rondas). *Verificação:* mínimo 8 acertos. ([[02-Ciclo-de-vida-dos-ficheiros|02]])
- [ ] **E3.** `.gitignore` que ignora `*.log` e `.env` mas permite `exemplo.env` (dica: negação `!`). *Verificação:* `git check-ignore -v` confirma cada caso. ([[03-gitignore-stash-restore|07]])
- [ ] **E4.** `stash` a meio de tarefa, troca de branch, `pop`. *Verificação:* zero perdas, `stash list` vazio no fim. ([[03-gitignore-stash-restore|07]])

## Intermédio (módulos 04–07)

- [ ] **E5.** Feature branch + `merge --no-ff` em `main` local. *Verificação:* `log --graph` mostra merge commit. ([[02-merge-rebase-cherry-pick|09]])
- [ ] **E6.** Publica repo no GitHub com SSH, protege `main`. *Verificação:* push direto recusado, só via PR. ([[02-SSH-e-autenticacao|04]], [[02-GitHub-Issues-releases-actions|11]])
- [ ] **E7.** PR com `Closes #N`, CI verde, review de colega, squash merge. *Verificação:* issue fechou sozinha. ([[01-pull-requests-e-code-review|12]])
- [ ] **E8.** Provoca conflito (mesma linha em 2 branches) e resolve. *Verificação:* `git diff --check` limpo + testes passam. ([[01-conflitos-e-recuperacao|13]])

## Avançado (módulos 08–09)

- [ ] **E9.** Atualiza feature com `rebase` + `push --force-with-lease`. *Verificação:* histórico linear, sem queixas da equipa. ([[02-merge-rebase-cherry-pick|09]], [[02-fetch-pull-push-remote-avancado|17]])
- [ ] **E10.** Commit errado com push → `revert`. Commit local mau → `reset --soft`. *Verificação:* justificas cada escolha em voz alta. ([[01-reset-revert-reflog|16]])
- [ ] **E11.** Apaga branch com `-D` e recupera via `reflog` em menos de 5 min. ([[01-reset-revert-reflog|16]])
- [ ] **E12.** Fork + `upstream`, PR para o original. *Verificação:* PR merged. ([[02-fetch-pull-push-remote-avancado|17]])

## Profissional (módulos 10–11)

- [ ] **E13.** Reescreve 5 mensagens para Conventional Commits; tag `v1.0.0`; release com notas. *Verificação:* changelog gerado faz sentido. ([[01-conventional-commits-semver-cicd|18]])
- [ ] **E14.** Sprint simulada do [[02-Workflow-Cuidar-Angola|15 — Cuidar Angola]] (issues → PRs → release). *Verificação:* equipa avalia o processo na retro.
- [ ] **E15.** Scan de segredos limpo (`gitleaks`) + assinatura GPG ativa. *Verificação:* commits "Verified". ([[02-seguranca-e-boas-praticas|19]])

## Avaliação final

**Perguntas de compreensão:**

1. Que exercício prova que distingues `add` de `commit`? E `fetch` de `pull`?
2. Que exercícios exigem repo descartável e porquê?
3. O que significa "só avança com critérios cumpridos" na prática?

**Desafio de interpretação:** um colega diz "completei E8" mas `git log --graph` não mostra merge e há marcadores no código. O que falhou? (Resposta: não concluiu — faltam `add`+`commit` e `diff --check`; reabrir o procedimento da lição 13.)

**Projetos guiados:** [[01-projetos-progressivos|20 — Projetos práticos]]
