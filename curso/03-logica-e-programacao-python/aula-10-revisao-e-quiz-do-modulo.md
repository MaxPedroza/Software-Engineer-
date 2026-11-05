# Aula 10 — Revisão e quiz do módulo

**Duração:** ~20 min · **Módulo 3**

## Resumo
- Algoritmo = passos finitos e claros; decomponha antes de codar.
- Tipos: `int`, `float`, `str`, `bool`; operadores `//`, `%`, `**`.
- `if/elif/else`, truthy/falsy, curto-circuito.
- `for` e `while`; `range` com fim exclusivo; `break`/`continue`.
- Funções: parâmetros padrão (nunca mutáveis), escopo LEGB, recursão com caso base.
- list, tuple, dict, set: escolha pela necessidade (ordem, mutabilidade, unicidade, busca).
- Módulos, pacotes, `venv` e `requirements.txt`.
- Arquivos com `with open`, JSON e CSV.
- Exceções específicas, `logging` e depuração metódica.

## Quiz (responda sem consultar)
1. Qual o resultado de `17 // 5`, `17 % 5` e `2 ** 3`?
2. O que `range(2, 10, 3)` gera?
3. Cite três valores falsy em Python.
4. Qual o problema de `def f(x, l=[])`?
5. O que significa a regra LEGB?
6. Qual a diferença entre lista e tupla?
7. Como remover duplicados de uma lista?
8. Por que usar `with open(...)`?
9. Qual a diferença entre `json.load` e `json.loads`?
10. Para que serve o bloco `finally`?

## Gabarito resumido
1. 3, 2 e 8 · 2. 2, 5, 8 · 3. `0`, `""`, `[]`, `None`, `False` (qualquer três) · 4. A lista padrão é criada uma vez e compartilhada entre chamadas · 5. Ordem de busca de nomes: Local, Enclosing, Global, Built-in · 6. Lista é mutável; tupla é imutável · 7. `list(set(l))` (ou `dict.fromkeys` para manter a ordem) · 8. Fecha o arquivo automaticamente, mesmo com erro · 9. `load` lê de arquivo; `loads` lê de string · 10. Executa sempre, com ou sem erro (limpeza)

## Entregável do módulo
**CLI de gerenciamento de tarefas** em Python: comandos `adicionar`, `listar`, `concluir` e `remover`, salvando em `tarefas.json`, com `argparse`, funções separadas, tratamento de erros (id inexistente, JSON corrompido) e um `README` com instruções de uso.

## Checklist final
- [ ] Acertei 8 ou mais questões
- [ ] A CLI funciona e trata erros
- [ ] Pronto para o Módulo 4
