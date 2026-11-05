# Aula 7 — Sistemas de numeração e aritmética binária

**Duração:** ~30 min · **Módulo 4**

## Objetivo
Converter entre bases 2, 10 e 16 e realizar aritmética binária, incluindo complemento de dois.

## Teoria
- Em base b, o dígito na posição i vale `dígito · bⁱ`. 1011₂ = 8 + 0 + 2 + 1 = 11.
- **Decimal → binário**: divisões sucessivas por 2, lendo os restos de baixo para cima. 13 → 1101.
- **Hexadecimal** (0–9, A–F): cada dígito hex = 4 bits. `0xFF` = 1111 1111 = 255. Usado em cores (`#FF8800`), endereços de memória, hashes.
- **Soma binária**: 0+0=0, 0+1=1, 1+1=10 (vai-um). 0101 + 0011 = 1000.
- **Complemento de dois** (inteiros com sinal em n bits): inverta os bits e some 1. Em 8 bits, −5 = 11111011. Faixa: −2ⁿ⁻¹ a 2ⁿ⁻¹−1 (−128 a 127). Estouro (overflow): 127 + 1 → −128.
- **Operações bit a bit**: `&`, `|`, `^`, `~`, `<<`, `>>`. `x << 1` multiplica por 2; `x & 1` testa se é ímpar; máscaras e flags.

## Exemplo em Python
```python
def para_base(n: int, base: int) -> str:
    digitos = "0123456789ABCDEF"
    if n == 0:
        return "0"
    saida = ""
    while n > 0:
        saida = digitos[n % base] + saida
        n //= base
    return saida

def de_base(texto: str, base: int) -> int:
    return sum("0123456789ABCDEF".index(c) * base ** i
               for i, c in enumerate(reversed(texto.upper())))

print(para_base(13, 2), para_base(255, 16))    # 1101 FF
print(de_base("1011", 2), de_base("FF", 16))   # 11 255
print(bin(13), hex(255), int("1101", 2), int("ff", 16))

def complemento_de_dois(n: int, bits: int = 8) -> str:
    return format(n & (2 ** bits - 1), f"0{bits}b")

print(complemento_de_dois(-5))        # 11111011
print(0b0101 + 0b0011 == 0b1000)      # True
print(6 & 3, 6 | 3, 6 ^ 3, 1 << 4)    # 2 7 5 16

PERM_LER, PERM_ESCREVER = 0b100, 0b010
perm = PERM_LER | PERM_ESCREVER
print(bool(perm & PERM_ESCREVER))     # True
```

## Exercício
1. Converta à mão 45 para binário e `0b101101` para hexadecimal; confira com Python.
2. Represente −20 em 8 bits (complemento de dois) e explique o que acontece com `127 + 1`.
3. Use máscaras para extrair os componentes R, G e B da cor `0xFF8800`.

## Checklist
- [ ] Converto entre binário, decimal e hexadecimal
- [ ] Somo números binários
- [ ] Entendo complemento de dois e operadores bit a bit
