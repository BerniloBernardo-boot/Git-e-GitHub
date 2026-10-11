# Padrão pedagógico do guia — como cada lição ensina

Este ficheiro define o modelo de ensino aplicado a todas as notas do repositório.
Serve para manter consistência quando criares ou reveres uma lição.

## 1. Sequência obrigatória de cada conceito

1. **Definição** — o que é, em linguagem simples (1–2 frases).
2. **Finalidade** — que problema resolve e porque existe.
3. **Funcionamento** — como opera internamente (objetos, refs, zonas afetadas).
4. **Representação visual** — diagrama Mermaid próximo do texto, com explicação bloco a bloco e seta a seta.
5. **Sintaxe** — estrutura do comando e significado de cada argumento, mesmo quando não há argumentos.
6. **Demonstração** — exemplo real e executável, explicado linha por linha.
7. **Estado antes e depois** — tabela ou lista do que mudou (working tree, staging, histórico, remoto).
8. **Prática** — exercício para executar no terminal, com dificuldade crescente.
9. **Verificação** — como confirmar o resultado (`status`, `log`, `diff`, `branch -vv`).
10. **Memorização** — regra curta, analogia ou associação mental.
11. **Avaliação** — 3 perguntas de compreensão + 1 exercício prático + 1 desafio de interpretação + resumo visual + checklist de domínio.

Nunca apresentar um comando isolado sem contexto, finalidade e resultado esperado.
Distinguir sempre exemplos simulados de resultados efetivamente observados.

## 2. Bloco-padrão de cada comando

```markdown
### Comando: `git exemplo`

**Selo:** [SEGURO] | [ATENCAO] | [DESTRUTIVO]
**Definição:** ...
**Quando utilizar:** ...
**Sintaxe:** `git exemplo [<argumento>]`
**O que significa cada parte:** ...
**Demonstração linha por linha:**
```bash
git exemplo ...
```
**Interpretação do resultado:** (exemplo assinalado como simulado)
**Antes / depois:** ...
**Erro frequente e correção:** ...
**Regra de memória:** ...
**Desafio:** ...
```

Selos de risco:

| Selo | Significado |
|---|---|
| [SEGURO] | Só lê ou cria dados sem apagar; usa sem medo |
| [ATENCAO] | Altera histórico local ou exige verificação prévia |
| [DESTRUTIVO] | Pode apagar trabalho permanentemente; verificar antes |

## 3. Regras visuais e editoriais

- Sem emojis no corpo das lições. Usar selos de texto e callouts (`[!NOTE]`, `[!TIP]`, `[!WARNING]`, `[!CAUTION]`).
- Títulos indicam o conceito; definições em destaque (`> **Definição:** ...`).
- Diagrama sempre colado à explicação correspondente, nunca como decoração.
- Blocos de código com linguagem identificada (`bash`, `text`, `gitignore`, `yaml`).
- Comparações lado a lado em tabela quando há conceitos semelhantes (`add` vs `commit`, `fetch` vs `pull`, `merge` vs `rebase`, `reset` vs `revert`).
- Secções distintas para Exemplo, Prática, Aviso e Avaliação.
- Português europeu claro; comandos e termos técnicos em inglês original.
- Exemplos verificados com Git recente no Linux; diferenças Windows/macOS assinaladas.

## 4. Avaliação no fim de cada lição

Toda a lição termina com:

- Três perguntas de compreensão (resposta curta).
- Um exercício prático com critério de conclusão observável.
- Um desafio de interpretação (prever resultado ou ler saída de terminal).
- Um resumo visual (tabela ou diagrama pequeno).
- Uma checklist de domínio (o que o aluno deve conseguir explicar e fazer).

Uma lição nunca se considera dominada só por ter sido lida: exige respostas e exercícios concluídos.

## 5. Segurança

- Explicar efeitos antes de recomendar execução, com destaque para `git reset --hard`, `git clean -fd`, `git push --force`, `git branch -D` e reescrita de histórico.
- Ensinar a verificar (`git status`, `git branch --show-current`, `git log --oneline -5`, `git stash list`) antes de qualquer comando [ATENCAO] ou [DESTRUTIVO].
- Nunca assumir que local e remoto estão iguais.
