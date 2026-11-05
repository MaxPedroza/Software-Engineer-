# Aula 2 — Bits, bytes e representação de dados

**Duração:** ~20 min · **Módulo 1**

## Objetivo
Entender como o computador representa números, texto e outros dados usando apenas 0 e 1.

## Teoria
- **Bit**: menor unidade (0 ou 1). **Byte** = 8 bits (256 valores possíveis, 0–255).
- **Binário** (base 2): cada posição vale uma potência de 2.
  `1011₂ = 1·8 + 0·4 + 1·2 + 1·1 = 11₁₀`
- **Hexadecimal** (base 16): usa 0–9 e A–F; 1 dígito hex = 4 bits. `0xFF = 255`. Muito usado em cores (`#FF8800`), endereços de memória e hashes.
- **Texto**: cada caractere mapeia para um número. **ASCII** cobre inglês (7 bits). **Unicode** cobre todos os idiomas e emojis; **UTF-8** é a codificação mais usada (1 a 4 bytes por caractere).
- **Inteiros negativos**: complemento de dois.
- **Decimais**: ponto flutuante (IEEE 754) — por isso `0.1 + 0.2 != 0.3` em muitas linguagens.
- **Imagens/áudio/vídeo**: sequências de números (pixels, amostras).

### Unidades
1 KB ≈ 1.000 bytes · 1 MB ≈ 1.000 KB · 1 GB ≈ 1.000 MB (KiB/MiB/GiB usam 1.024).

## Exemplo em Python
```python
print(bin(11))            # 0b1011
print(int("1011", 2))     # 11
print(hex(255))           # 0xff
print(ord("A"), chr(66))  # 65 B
print("ação".encode("utf-8"))  # b'a\xc3\xa7\xc3\xa3o'
print(0.1 + 0.2)          # 0.30000000000000004
```

## Exercício
1. Converta à mão 42 para binário e `0b110101` para decimal.
2. Quantos valores diferentes cabem em 2 bytes?
3. Rode o exemplo acima e explique por que "ação" tem mais bytes que caracteres.

## Checklist
- [ ] Converto entre decimal, binário e hexadecimal
- [ ] Sei o que é UTF-8
- [ ] Entendo por que decimais podem ter imprecisão
