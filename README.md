# Git e GitHub — Guia Profissional de Estudo

> Guia completo e gratuito de Git e GitHub, **do zero ao nível profissional**, em português. Criado para estudo individual e em equipa — incluindo o workflow real do projeto **Cuidar Angola** (`main` → produção, `develop` → integração, `feature/*` → tarefas).

## O que este repositório contém

- 📚 **24 notas de estudo** organizadas em 15 módulos progressivos (iniciante → intermédio → avançado → profissional)
- 🧭 **Todos os comandos explicados**: sintaxe, funcionamento interno, quando usar, exemplo executável, resultado esperado, erros frequentes, riscos (🟢 seguro / 🟡 cuidado / 🔴 destrutivo) e alternativas
- 📊 **19 diagramas Mermaid**: ciclo de vida dos ficheiros, branches, merge vs. rebase, Pull Requests, conflitos, CI/CD e colaboração frontend ↔ backend
- 👥 **Workflow de equipa pronto a usar** (pasta `08-Workflows-Profissionais`)
- 🏋️ **Projetos práticos e 15 exercícios** com critérios de conclusão
- ⚡ **Cheat-sheet** de referência rápida + **glossário** com 30 termos

## Como estudar

| Nível | Módulos | Objetivo |
|---|---|---|
| 🟢 Iniciante | 01 → 03 | Conceitos, instalação, primeiros commits |
| 🟡 Intermédio | 04 → 07 | Branches, GitHub, PRs, conflitos |
| 🟠 Avançado | 08 → 09 | Workflows, rebase, reset/reflog |
| 🔴 Profissional | 10 → 11 | Segurança, CI/CD, projetos em equipa |

**Começa aqui:** abre a nota `README-Obsidian.md` (índice navegável) ou entra em `01-Fundamentos/`.

> [!NOTE]
> Compatível com [Obsidian](https://obsidian.md) (links `[[...]]`, callouts e Mermaid funcionam nativamente — basta abrir esta pasta como vault). No GitHub, os ficheiros leem-se normalmente; os links internos usam sintaxe wiki do Obsidian.

## Índice

### Fundamentos e configuração
- [01 — O que é Git e GitHub](01-Fundamentos/01-O-que-e-Git-e-GitHub.md)
- [02 — Ciclo de vida dos ficheiros](01-Fundamentos/02-Ciclo-de-vida-dos-ficheiros.md)
- [03 — Instalação e configuração inicial](02-Instalacao-e-Configuracao/01-Instalacao-e-configuracao-inicial.md)
- [04 — SSH e autenticação](02-Instalacao-e-Configuracao/02-SSH-e-autenticacao.md)

### Comandos essenciais
- [05 — init, clone, status, add, commit](03-Comandos-Essenciais/01-init-clone-status-add-commit.md)
- [06 — log, diff, show](03-Comandos-Essenciais/02-log-diff-show.md)
- [07 — .gitignore, stash, restore](03-Comandos-Essenciais/03-gitignore-stash-restore.md)

### Branches e colaboração
- [08 — Branches, switch, checkout](04-Branches-e-Merge/01-branches-switch-checkout.md)
- [09 — merge, rebase, cherry-pick](04-Branches-e-Merge/02-merge-rebase-cherry-pick.md)
- [10 — Repositórios, remotes, tags](05-GitHub-e-Repositorios/01-repositorios-remotes-tags.md)
- [11 — Issues, releases, Actions](05-GitHub-e-Repositorios/02-GitHub-Issues-releases-actions.md)
- [12 — Pull Requests e code review](06-Pull-Requests-e-Code-Review/01-pull-requests-e-code-review.md)
- [13 — Conflitos e recuperação](07-Resolucao-de-Conflitos/01-conflitos-e-recuperacao.md)

### Nível profissional
- [14 — Git Flow, GitHub Flow, trunk-based](08-Workflows-Profissionais/01-git-flow-github-flow-trunk-based.md)
- [15 — Workflow real: Cuidar Angola ⭐](08-Workflows-Profissionais/02-Workflow-Cuidar-Angola.md)
- [16 — reset, revert, reflog](09-Git-Avancado/01-reset-revert-reflog.md)
- [17 — fetch, pull, push, remote (avançado)](09-Git-Avancado/02-fetch-pull-push-remote-avancado.md)
- [18 — Conventional Commits, SemVer, CI/CD](10-Seguranca-e-Boas-Praticas/01-conventional-commits-semver-cicd.md)
- [19 — Segurança e boas práticas](10-Seguranca-e-Boas-Praticas/02-seguranca-e-boas-praticas.md)

### Prática e referência
- [20 — Projetos práticos](11-Projetos-Praticos/01-projetos-progressivos.md)
- [21 — Erros comuns](12-Erros-Comuns/01-erros-comuns-e-solucoes.md)
- [22 — Referência rápida ⚡](13-Referencia-Rapida/01-cheat-sheet.md)
- [23 — Exercícios](14-Exercicios/01-exercicios-por-nivel.md)
- [24 — Glossário](15-Glossario/01-glossario.md)

## Legenda de risco dos comandos

| Selo | Significado |
|---|---|
| 🟢 Seguro | Não altera histórico nem perde dados |
| 🟡 Cuidado | Altera histórico local ou exige atenção |
| 🔴 Destrutivo | Pode apagar dados permanentemente |

## Contribuir

Queres melhorar o guia? Lê o [CONTRIBUTING.md](CONTRIBUTING.md) — contributos via Pull Request são bem-vindos.

## Licença

[MIT](LICENSE) — usa, partilha e adapta livremente para estudo.
