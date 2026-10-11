# Índice do guia (Obsidian)

> Este ficheiro é o índice navegável dentro do Obsidian. No GitHub, o índice principal está no [README.md](README.md).
> O padrão de ensino de cada lição está em [[PADRAO-PEDAGOGICO|Padrão pedagógico]].

## Percurso de aprendizagem

| Nível | Módulos | Objetivo |
|---|---|---|
| Iniciante | 01 → 03 | Entender conceitos, instalar, primeiros commits |
| Intermédio | 04 → 07 | Branches, GitHub, PRs, conflitos |
| Avançado | 08 → 09 | Workflows, rebase, reset/reflog |
| Profissional | 10 → 11 | Segurança, CI/CD, projetos em equipa |

Regra: só avança de nível com os checklists de domínio cumpridos (não basta ler — responde e pratica).

## Notas

### Fundamentos e configuração
- [[01-O-que-e-Git-e-GitHub|01 — O que é Git e GitHub]]
- [[02-Ciclo-de-vida-dos-ficheiros|02 — Ciclo de vida dos ficheiros]]
- [[01-Instalacao-e-configuracao-inicial|03 — Instalação e configuração inicial]]
- [[02-SSH-e-autenticacao|04 — SSH e autenticação]]

### Comandos essenciais
- [[01-init-clone-status-add-commit|05 — init, clone, status, add, commit]]
- [[02-log-diff-show|06 — log, diff, show]]
- [[03-gitignore-stash-restore|07 — .gitignore, stash, restore]]

### Branches e colaboração
- [[01-branches-switch-checkout|08 — Branches, switch, checkout]]
- [[02-merge-rebase-cherry-pick|09 — merge, rebase, cherry-pick]]
- [[01-repositorios-remotes-tags|10 — Repositórios, remotes, tags]]
- [[02-GitHub-Issues-releases-actions|11 — Issues, releases, Actions]]
- [[01-pull-requests-e-code-review|12 — Pull Requests e code review]]
- [[01-conflitos-e-recuperacao|13 — Conflitos e recuperação]]

### Nível profissional
- [[01-git-flow-github-flow-trunk-based|14 — Git Flow, GitHub Flow, trunk-based]]
- [[02-Workflow-Cuidar-Angola|15 — Workflow real: Cuidar Angola]]
- [[01-reset-revert-reflog|16 — reset, revert, reflog]]
- [[02-fetch-pull-push-remote-avancado|17 — fetch, pull, push, remote (avançado)]]
- [[01-conventional-commits-semver-cicd|18 — Conventional Commits, SemVer, CI/CD]]
- [[02-seguranca-e-boas-praticas|19 — Segurança e boas práticas]]

### Prática e referência
- [[01-projetos-progressivos|20 — Projetos práticos]]
- [[01-erros-comuns-e-solucoes|21 — Erros comuns]]
- [[01-cheat-sheet|22 — Referência rápida]]
- [[01-exercicios-por-nivel|23 — Exercícios]]
- [[01-glossario|24 — Glossário]]

## Legenda de risco dos comandos

| Selo | Significado |
|---|---|
| [SEGURO] | Não altera histórico nem perde dados |
| [ATENCAO] | Altera histórico local ou exige atenção |
| [DESTRUTIVO] | Pode apagar dados permanentemente |

> [!NOTE]
> Exemplos verificados com Git recente no Linux; saídas marcadas como "exemplo simulado" são representativas, não cópias literais. Diferenças para Windows/macOS estão assinaladas onde relevante.
