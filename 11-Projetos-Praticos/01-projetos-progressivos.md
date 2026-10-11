# 20 — Projetos práticos progressivos

> **Nível:** todos · Sem serviços pagos. Cada projeto tem objetivo, passos e critério de "feito".

## Projeto 1 — Diário Git (individual, 🟢)

**Objetivo:** ciclo básico no sangue.
1. `git init -b main diario`, `.gitignore` (ex.: `privado/`).
2. Um commit por dia durante 7 dias (`docs(diario): dia N`).
3. Pratica `status`, `diff`, `log --oneline --graph`.
✅ **Feito:** 7 commits, `git log` conta a semana.

## Projeto 2 — Site estático com releases (individual, 🟡)

**Objetivo:** tags + GitHub + Pages.
1. Página HTML/CSS simples; push para GitHub.
2. Ativa **Settings → Pages** (grátis) para publicar.
3. 3 features em branches + PRs (squash merge) + releases `v1.0.0`→`v1.2.0`.
✅ **Feito:** site no ar + 3 tags + histórico limpo.

## Projeto 3 — Simular equipa (2+ pessoas ou 2 clones, 🟡→🟠)

**Objetivo:** conflitos, PRs, review.
1. Um repo, dois clones (ou conta de colega).
2. Ambos editam a mesma função → PRs → conflito → resolve ([[01-conflitos-e-recuperacao|guia]]).
3. Alternam papéis autora/revisora com checklist de [[01-pull-requests-e-code-review|review]].
✅ **Feito:** 2 PRs merged com review real + 1 conflito resolvido.

## Projeto 4 — Cuidar Angola mini-sprint (equipa, 🟠→🔴)

**Objetivo:** aplicar o [[02-Workflow-Cuidar-Angola|workflow real]].
1. Proteger `develop` (PR + CI com linter grátis).
2. Sprint de 1 semana: issues → `feature/*` → PRs → `develop`.
3. Release `v0.1.0` em `main` com notas.
✅ **Feito:** release publicada, zero pushes diretos, retro documentada.

## Projeto 5 — Resgate (individual, 🟠)

**Objetivo:** recuperação sem medo (repo de teste descartável!).
1. Provoca: commit mau, `reset --hard` "acidental", branch apagado com `-D`.
2. Recupera tudo via `reflog` + `revert` ([[01-reset-revert-reflog|guia]]).
✅ **Feito:** histórico final correto + relato do que fizeste.

**Ver também:** [[01-exercicios-por-nivel|Exercícios por nível]]
