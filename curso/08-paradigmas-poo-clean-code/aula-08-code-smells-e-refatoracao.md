# Aula 8 — Code smells e refatoração

**Duração:** ~25 min · **Módulo 8**

## Objetivo
Identificar sinais de código problemático e refatorar com segurança.

## Teoria
**Code smell**: indício de problema de design (não é bug). Exemplos:
- **Método longo** e **classe gigante** (God Class)
- **Código duplicado**
- **Lista longa de parâmetros**
- **Feature envy**: método usa mais dados de outra classe do que da sua
- **Switch/if em cadeia** por tipo
- **Números mágicos** e **primitive obsession**

**Refatoração** = mudar a estrutura interna sem alterar o comportamento observável. Sempre com **testes verdes** antes e depois, em passos pequenos.
Técnicas: *Extract Function*, *Rename*, *Replace Conditional with Polymorphism*, *Introduce Parameter Object*, *Move Method*.

## Exemplo em Python
Antes (switch por tipo + duplicação):
```python
def frete(tipo, peso):
    if tipo == "normal":
        return peso * 2
    elif tipo == "expresso":
        return peso * 5 + 10
    raise ValueError(tipo)
```
Depois (polimorfismo / tabela):
```python
from dataclasses import dataclass

@dataclass(frozen=True)
class Frete:
    por_kg: float
    taxa: float = 0.0
    def calcular(self, peso: float) -> float:
        return peso * self.por_kg + self.taxa

FRETES = {"normal": Frete(2), "expresso": Frete(5, 10)}

def frete(tipo: str, peso: float) -> float:
    return FRETES[tipo].calcular(peso)

assert frete("expresso", 3) == 25   # comportamento preservado
```

## Exercício
1. Escreva testes para a função `frete` original antes de refatorar.
2. Encontre 3 code smells em um script seu e nomeie a técnica que resolve cada um.
3. Aplique *Introduce Parameter Object* em uma função com 5 parâmetros.

## Checklist
- [ ] Reconheço pelo menos 5 code smells
- [ ] Só refatoro com testes protegendo o comportamento
- [ ] Faço passos pequenos e commits frequentes
