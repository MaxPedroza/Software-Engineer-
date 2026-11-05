# Aula 8 — Como um programa é executado

**Duração:** ~20 min · **Módulo 1**

## Objetivo
Seguir a jornada completa: do código-fonte à execução na CPU.

## Teoria
1. **Escrita**: você cria o código-fonte.
2. **Tradução**: compilador/interpretador gera código de máquina ou bytecode.
3. **Carregamento**: o SO (*loader*) lê o executável do disco, cria um **processo** e mapeia o programa na memória.
4. **Layout de memória do processo**:
   - **Code/Text**: instruções
   - **Data**: variáveis globais
   - **Heap**: memória dinâmica (objetos, listas)
   - **Stack (pilha)**: chamadas de função e variáveis locais
5. **Execução**: a CPU executa o ciclo buscar–decodificar–executar usando o *program counter*.
6. **Chamadas ao SO**: E/S (arquivos, rede) via syscalls.
7. **Término**: o processo devolve um *exit code* (0 = sucesso).

### Stack vs Heap
| Stack | Heap |
|-------|------|
| Rápida, automática | Mais flexível, gerenciada (GC) ou manual |
| Tamanho limitado (*stack overflow*) | Pode crescer; *memory leak* se não liberada |

### Bibliotecas
Programas usam bibliotecas estáticas (embutidas) ou dinâmicas (`.so`, `.dll`) carregadas na execução.

## Exercício
1. Escreva uma função recursiva sem caso base em Python e observe o `RecursionError`. Relacione com a stack.
2. Rode `echo $?` após um comando que falha e outro que funciona. O que significa?

## Checklist
- [ ] Descrevo as etapas do código à execução
- [ ] Diferencio stack e heap
- [ ] Sei o que é exit code
