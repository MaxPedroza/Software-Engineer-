# Aula 7 — Compiladores vs interpretadores

**Duração:** ~20 min · **Módulo 1**

## Objetivo
Entender como código-fonte vira algo executável e as consequências para cada linguagem.

## Teoria
O processador só entende **código de máquina**. Linguagens de alto nível precisam ser traduzidas.

| Abordagem | Como funciona | Exemplos |
|-----------|---------------|----------|
| **Compilada (AOT)** | Traduz tudo antes, gera executável | C, C++, Go, Rust |
| **Interpretada** | Lê e executa linha a linha | Python, Ruby (clássico) |
| **Bytecode + VM** | Compila para bytecode, executa em máquina virtual | Java (JVM), C# (.NET), Python (CPython) |
| **JIT** | VM compila trechos "quentes" em tempo de execução | V8 (JavaScript), JVM |

### Etapas de um compilador
Análise léxica (tokens) → sintática (árvore AST) → semântica (tipos) → otimização → geração de código.

### Trade-offs
- Compilada: geralmente mais rápida, erros de tipo detectados cedo, executável por plataforma.
- Interpretada: desenvolvimento ágil, portável, mais lenta.
- Linguagens não são "compiladas ou interpretadas" por natureza; é uma característica da *implementação*.

## Exemplo
```python
import dis
def soma(a, b): return a + b
dis.dis(soma)   # mostra o bytecode do CPython
```

## Exercício
1. Compile um "Olá, mundo" em C (`gcc hello.c -o hello`) e rode o executável; compare com `python hello.py`.
2. Rode `dis.dis` em uma função sua e descreva as instruções.

## Checklist
- [ ] Diferencio compilação, interpretação, bytecode e JIT
- [ ] Sei citar as etapas de um compilador
- [ ] Entendo os trade-offs de cada abordagem
