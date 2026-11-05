# Aula 1 — Requisitos funcionais, não funcionais e estimativas de capacidade

**Duração:** ~25 min · **Módulo 17**

## Objetivo
Levantar requisitos e fazer estimativas de ordem de grandeza (back-of-the-envelope) antes de desenhar um sistema.

## Teoria
- **Requisitos funcionais (RF)**: o que o sistema faz ("o usuário encurta uma URL").
- **Requisitos não funcionais (RNF)**: como ele se comporta — latência, disponibilidade, durabilidade, consistência, custo, segurança.
- Sempre defina **escopo** e **o que fica de fora** no início de um design.

### Números úteis
| Item | Valor aproximado |
|------|------------------|
| Segundos por dia | ~86.400 (≈ 10⁵) |
| Leitura em memória | ~100 ns |
| Leitura SSD | ~100 µs |
| Round-trip no mesmo datacenter | ~0,5 ms |
| Round-trip entre continentes | ~150 ms |

### Fórmulas
- QPS médio = requisições/dia ÷ 86.400; **pico ≈ 2–5× a média**.
- Armazenamento = itens/dia × tamanho × dias de retenção × fator de replicação.
- Banda = QPS × tamanho médio da resposta.

## Exemplo: encurtador de URL
```python
novas_por_dia = 100_000_000
leitura_por_escrita = 10

qps_escrita = novas_por_dia / 86_400          # ~1.157/s
qps_leitura = qps_escrita * leitura_por_escrita  # ~11.570/s
pico_leitura = qps_leitura * 3

bytes_por_registro = 500
armazenamento_5_anos_tb = novas_por_dia * 365 * 5 * bytes_por_registro / 1e12

print(round(qps_escrita), round(qps_leitura), round(pico_leitura))
print(f"{armazenamento_5_anos_tb:.0f} TB")  # ~91 TB (sem replicação)
```

## Exercício
1. Estime QPS e armazenamento de um app de chat com 50 milhões de usuários ativos/dia, 40 mensagens/usuário/dia, 200 bytes por mensagem, retenção de 1 ano.
2. Escreva 3 RNFs mensuráveis (ex.: p99 < 200 ms, disponibilidade 99,95%) para o projeto contínuo.

## Checklist
- [ ] Separo RF de RNF
- [ ] Sei estimar QPS, armazenamento e banda
- [ ] Defino escopo e metas mensuráveis
