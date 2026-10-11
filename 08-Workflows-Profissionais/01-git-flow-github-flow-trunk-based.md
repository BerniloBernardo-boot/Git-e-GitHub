# 14 — Git Flow, GitHub Flow, trunk-based

> **Nível:** Avançado · **Pré-requisitos:** [[02-merge-rebase-cherry-pick|09]], [[01-pull-requests-e-code-review|12]] · **Tempo estimado:** 60 min
> **Objetivo:** escolher o workflow certo para cada contexto e justificar a escolha com critérios objetivos.

## 1. Definição e finalidade

> **Definição:** um workflow de branches é a convenção que diz onde o código nasce, onde é revisto e de onde sai para produção.

**Finalidade:** sem convenção, cada pessoa integra onde quer — `main` parte, releases atrasam, hotfixes perdem-se. O workflow transforma "hábitos individuais" em "processo de equipa".

## 2. Visão geral (comparação direta)

| | Git Flow | GitHub Flow | Trunk-based |
|---|---|---|---|
| Branches | `main`, `develop`, `feature/*`, `release/*`, `hotfix/*` | `main` + `feature/*` (PR direto para main) | `main` (+ branches curtíssimos de 1–2 dias) |
| Releases | Ciclos planeados via `release/*` | Deploy contínuo de `main` | Deploy contínuo, feature flags |
| Complexidade | Alta (muitos branches) | Baixa | Baixíssima (exige disciplina + CI forte) |
| Ideal para | Software versionado (apps, libs, releases rígidas) | Web apps com deploy frequente, equipas pequenas/médias | Equipas seniores, CI/CD maduro, deploys diários |

```mermaid
gitGraph
    commit id: "v1.0"
    branch develop
    commit id: "integracao"
    branch feature/A
    commit id: "trabalho"
    checkout develop
    merge feature/A id: "merge A"
    branch release/1.1
    commit id: "estabiliza"
    checkout main
    merge release/1.1 id: "v1.1"
```

Leitura: `feature/A` nasce de `develop` e volta via merge; `release/1.1` estabiliza (só fixes) e faz merge em `main` **e** `develop` para nada se perder.

## 3. Cada workflow em detalhe

### Git Flow

- `main`: só código lançado (tags `v*`).
- `develop`: integração diária.
- `feature/*` ← `develop`, volta para `develop` via PR.
- `release/*`: estabilização (só fixes), depois merge em `main` **e** `develop`.
- `hotfix/*` ← `main`, volta para `main` **e** `develop`.

**Quando usar:** precisas de releases versionadas paralelas à continuação do desenvolvimento (caso do [[02-Workflow-Cuidar-Angola|15 — Cuidar Angola]]).

### GitHub Flow

1. Branch `feature/*` a partir de `main`.
2. Commits + push + PR.
3. Review + CI verde → merge → **deploy imediato de `main`**.

**Quando usar:** produto web com deploy contínuo, sem "janelas de release".

### Trunk-based development

- Todos integram em `main` (trunk) pelo menos 1x/dia.
- Features incompletas escondidas com **feature flags**, não com branches longos.
- Exige: CI rápido e fiável, testes bons, pair/mob programming.

**Quando usar:** equipas experientes com deploys múltiplos por dia. **Não recomendado** para equipas a aprender Git (conflitos constantes punem iniciantes).

## 4. Como escolher (árvore de decisão)

```mermaid
flowchart TD
    Q1{"Precisas de releases versionadas\nparalelas ao desenvolvimento?"} -->|sim| GF["Git Flow"]
    Q1 -->|nao| Q2{"Deploys continuos\nde main?"}
    Q2 -->|sim, equipa pequena/media| GHF["GitHub Flow"]
    Q2 -->|sim, varios deploys/dia\n+ CI maduro| TBD["Trunk-based"]
    Q2 -->|nao, trabalho simples| GHF
```

> [!TIP]
> Para o projeto Cuidar Angola (frontend + backend, equipa em aprendizagem, produção estável): **Git Flow simplificado** — `main` / `develop` / `feature/*` (+ `hotfix/*`). Detalhe completo em [[02-Workflow-Cuidar-Angola|15 — Workflow Cuidar Angola]].

**Regra de memória:** "Releases paralelas = Git Flow; deploy contínuo simples = GitHub Flow; deploys diários com equipa sénior = trunk."

## 5. Prática guiada

1. Para 3 cenários (app mobile com lojas, SaaS web com deploy diário, equipa de 2 em MVP), escolhe o workflow e justifica em 3 linhas cada.
2. Desenha o Git Flow simplificado de memória e compara com o diagrama acima.

## 6. Avaliação

**Perguntas de compreensão:**

1. Onde nasce e onde morre uma `feature/*` no Git Flow? E no GitHub Flow?
2. Para que serve `release/*` e porque faz merge em dois branches?
3. Porque o trunk-based é desaconselhado para equipas a aprender Git?

**Exercício prático:** dado um projeto real teu, escolhe o workflow e escreve as 5 regras de branch que a equipa seguirá.

**Desafio de interpretação:** equipa com deploys semanais versionados e hotfixes urgentes em produção. Qual workflow e porquê? (Resposta: Git Flow — `release/*` estabiliza sem travar `develop`, `hotfix/*` sai de `main`.)

**Resumo visual:**

| Cenário | Workflow |
|---|---|
| Releases versionadas + hotfixes | Git Flow |
| Web app, deploy contínuo | GitHub Flow |
| Deploys diários, CI maduro | Trunk-based |

**Checklist de domínio:**

- [ ] Justificas a escolha de workflow para 3 cenários diferentes.
- [ ] Desenhas o Git Flow simplificado de memória.
- [ ] Explicas o papel de cada tipo de branch.

**Próximo:** [[02-Workflow-Cuidar-Angola|15 — Workflow Cuidar Angola]]
