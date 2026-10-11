# 20 — Projetos práticos progressivos

> **Nível:** todos · **Pré-requisitos:** lições do nível correspondente · **Tempo estimado:** 1–4 semanas no total
> **Objetivo:** consolidar cada nível com um projeto completo e demonstrável. Sem serviços pagos.
> **Regra:** cada projeto usa o que os anteriores ensinaram; só avança com o critério de "feito" cumprido.

## Projeto 1 — Diário Git (individual, nível Iniciante)

**Objetivo:** ciclo básico no sangue (`status` → `add` → `commit` → `log`).
**Passos:**

1. `git init -b main diario`, cria `.gitignore` (ex.: `privado/`).
2. Um commit por dia durante 7 dias (`docs(diario): dia N`).
3. Pratica `status --short`, `diff` vs. `diff --staged`, `log --oneline --graph`.

**Critério de "feito":** 7 commits; `git log` conta a semana; explicas cada estado de ficheiro.
**Verificação:** `git log --oneline | wc -l` mostra 7; `git status --short` vazio (limpo).

## Projeto 2 — Site estático com releases (individual, nível Intermédio)

**Objetivo:** tags + GitHub + Pages + PRs.
**Passos:**

1. Página HTML/CSS simples; `remote add` + push para GitHub (lição [[01-repositorios-remotes-tags|10]]).
2. Ativa **Settings → Pages** (grátis) para publicar.
3. 3 features em branches + PRs (squash merge) + releases `v1.0.0` → `v1.2.0` (lições [[01-pull-requests-e-code-review|12]], [[02-GitHub-Issues-releases-actions|11]]).

**Critério de "feito":** site no ar + 3 tags anotadas + histórico legível em Conventional Commits.

## Projeto 3 — Simular equipa (2+ pessoas ou 2 clones, Intermédio para Avançado)

**Objetivo:** conflitos, PRs, review com checklist.
**Passos:**

1. Um repo, dois clones (ou conta de colega).
2. Ambos editam a mesma função → PRs → conflito → resolve ([[01-conflitos-e-recuperacao|13]]).
3. Alternam papéis autora/revisora com checklist de [[01-pull-requests-e-code-review|12]].

**Critério de "feito":** 2 PRs merged com review real + 1 conflito resolvido com `diff --check` limpo.

## Projeto 4 — Cuidar Angola mini-sprint (equipa, Avançado para Profissional)

**Objetivo:** aplicar o [[02-Workflow-Cuidar-Angola|workflow real]].
**Passos:**

1. Proteger `develop` (PR + CI com linter grátis).
2. Sprint de 1 semana: issues → `feature/*` → PRs → `develop` (lições [[01-git-flow-github-flow-trunk-based|14]], [[02-Workflow-Cuidar-Angola|15]]).
3. Release `v0.1.0` em `main` com notas (lição [[01-conventional-commits-semver-cicd|18]]).

**Critério de "feito":** release publicada, zero pushes diretos, retro documentada.

## Projeto 5 — Resgate (individual, Avançado)

**Objetivo:** recuperação sem medo — **sempre em repo de teste descartável!**
**Passos:**

1. Provoca: commit mau, `reset --hard` "acidental", branch apagado com `-D`.
2. Recupera tudo via `reflog` + `revert` ([[01-reset-revert-reflog|16]]).
3. Escreve relato: o que fizeste, porquê, como verificaste.

**Critério de "feito":** histórico final correto + relato reproduzível por outra pessoa.

## Avaliação global

**Perguntas de compreensão:**

1. Que lições cada projeto consolida? Porque esta ordem?
2. O que distingue "projeto feito" de "projeto lido"?
3. Que evidências (logs, URLs, tags) provam cada critério?

**Desafio:** escolhe um projeto e estima em 5 linhas o plano da primeira sessão de 1 hora.

**Checklist de domínio:**

- [ ] Completaste os projetos do teu nível com critérios verificados.
- [ ] Consegues demonstrar cada resultado (`log`, tags, PRs, releases) sem consultar notas.

**Ver também:** [[01-exercicios-por-nivel|23 — Exercícios por nível]]
