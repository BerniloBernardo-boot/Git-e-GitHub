# 12 — Pull Requests e code review

> **Nível:** 🟡 Intermédio · **Selo:** 🟢 Seguro

## 1. O que é um Pull Request

Pedido para integrar um branch noutro, com **revisão, CI e discussão** antes do merge. No GitHub, PRs são o portão de qualidade para `main`/`develop`.

```mermaid
sequenceDiagram
    participant A as "Autora (feature/*)"
    participant GH as "GitHub (PR)"
    participant CI as "Actions (CI)"
    participant R as Revisor
    A->>GH: push feature/* + abre PR p/ develop
    GH->>CI: corre testes/lint
    CI-->>GH: ✅ verde / ❌ vermelho
    R->>GH: review (approve / request changes / comment)
    GH->>GH: merge (merge/squash/rebase) após aprovações
    Note over A,GH: branch apagado após merge
```

## 2. Ciclo de vida de um PR (passo a passo)

```bash
git switch -c feature/login-validacao
# ... trabalha e commita ...
git push -u origin feature/login-validacao
# No GitHub: Compare & pull request → base: develop → título + descrição + Closes #12
```

1. **Abrir:** base correta (`develop`, não `main` — ver [[02-Workflow-Cuidar-Angola|Cuidar Angola]]), título claro, descrição com contexto + testes feitos.
2. **CI:** espera o verde; vermelho bloqueia (não peças review com CI quebrado).
3. **Review:** responde a cada comentário; `Resolve conversation` quando tratado.
4. **Atualizar:** se a base avançou → `git merge develop` na feature (ou `rebase`, só se privado e combinado).
5. **Merge:** métodos abaixo. **Apaga o branch** após o merge (botão Delete branch).

### Métodos de merge no GitHub

| Método | Resultado | Quando usar |
|---|---|---|
| **Merge commit** | Preserva todos os commits + commit de merge | Histórico fiel (padrão do Git Flow) |
| **Squash and merge** | 1 commit só na base | Features com commits "wip" sujos; mensagem final limpa |
| **Rebase and merge** | Commits reaplicados, linear | Equipas que exigem histórico linear |

## 3. Code review profissional

**Como autora:**
- PR pequeno (< 400 linhas idealmente), focado numa coisa.
- Template: o quê / porquê / como testar / riscos.

**Como revisora — checklist:**

- [ ] O código faz o que o PR diz? Há testes?
- [ ] Nomes claros? Funções pequenas?
- [ ] Segredos/credenciais expostos? (ver [[02-seguranca-e-boas-praticas|Segurança]])
- [ ] Quebras de compatibilidade / migrações?
- [ ] Comentários: pergunta antes de exigir (`sugestão:` vs. `bloqueador:`).

> [!TIP]
> Review não é caça a typos — o linter faz isso. Foca em lógica, segurança e manutenibilidade.

## 4. Erros frequentes

| Erro | Solução |
|---|---|
| PR para a base errada (`main` em vez de `develop`) | Edit → Change base (só sem conflitos graves) |
| PR gigante com 50 commits | Divide em PRs menores; usa squash no fim se permitido |
| `This branch has conflicts` | Atualiza a feature com a base e resolve ([[01-conflitos-e-recuperacao|Conflitos]]) |
| Merge sem aprovação em branch protegido | Impossível por design — pede review |

## Critérios de conclusão
- [ ] Abres um PR completo (descrição + issue ligada + CI) e fazes merge com o método adequado.
- [ ] Fazes uma review útil com pelo menos 1 bloqueador e 1 sugestão.

**Próximo:** [[01-conflitos-e-recuperacao|Conflitos e recuperação]] · **Workflow real:** [[02-Workflow-Cuidar-Angola|Cuidar Angola]]
