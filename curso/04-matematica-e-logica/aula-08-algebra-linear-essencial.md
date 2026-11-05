# Aula 8 — Álgebra linear essencial (vetores e matrizes)

**Duração:** ~30 min · **Módulo 4**

## Objetivo
Operar com vetores e matrizes, base de gráficos, ciência de dados e aprendizado de máquina.

## Teoria
- **Vetor**: lista ordenada de números; representa ponto, direção ou *features* (ex.: [altura, peso]).
- Operações: soma e subtração (componente a componente), multiplicação por escalar, **produto escalar** a·b = Σ aᵢbᵢ, norma ‖a‖ = √(a·a).
- Similaridade: cos θ = (a·b)/(‖a‖‖b‖) — usada em busca semântica e recomendação.
- **Matriz**: tabela m×n (linhas × colunas). Representa imagens, transformações (rotação, escala) e sistemas lineares.
- Soma de matrizes: mesmas dimensões, elemento a elemento. **Transposta** Aᵀ troca linhas por colunas.
- **Produto** A(m×n)·B(n×p) = C(m×p): Cᵢⱼ = Σ Aᵢₖ·Bₖⱼ. Só existe se colunas de A = linhas de B; **não é comutativo**.
- **Identidade** I: A·I = A. Determinante ≠ 0 → matriz inversível.

## Exemplo em Python
```python
import math

def soma(a, b):
    return [x + y for x, y in zip(a, b)]

def escalar(a, b):
    return sum(x * y for x, y in zip(a, b))

def norma(a):
    return math.sqrt(escalar(a, a))

def cosseno(a, b):
    return escalar(a, b) / (norma(a) * norma(b))

def transposta(m):
    return [list(col) for col in zip(*m)]

def produto(a, b):
    if len(a[0]) != len(b):
        raise ValueError("dimensões incompatíveis")
    bt = transposta(b)
    return [[escalar(linha, col) for col in bt] for linha in a]

u, v = [1, 2, 3], [4, 5, 6]
print(soma(u, v), escalar(u, v), round(norma(u), 3))   # [5,7,9] 32 3.742
print(round(cosseno([1, 0], [0, 1]), 3))               # 0.0 (perpendiculares)

A = [[1, 2], [3, 4]]
B = [[0, 1], [1, 0]]
print(produto(A, B))        # [[2, 1], [4, 3]]
print(produto(B, A))        # [[3, 4], [1, 2]] → não comutativo
print(transposta([[1, 2, 3], [4, 5, 6]]))
```

## Exercício
1. Calcule o ângulo entre [1, 1] e [1, 0] com `math.acos` (resposta: 45°).
2. Multiplique uma matriz 2×3 por uma 3×2 e diga o formato do resultado.
3. Escreva `identidade(n)` e confirme que `produto(A, identidade(2)) == A`.

## Checklist
- [ ] Calculo produto escalar e norma
- [ ] Multiplico matrizes e verifico dimensões
- [ ] Entendo transposta e identidade
