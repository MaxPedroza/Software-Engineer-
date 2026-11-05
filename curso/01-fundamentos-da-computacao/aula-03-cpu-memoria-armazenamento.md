# Aula 3 — CPU, memória RAM e armazenamento

**Duração:** ~20 min · **Módulo 1**

## Objetivo
Conhecer os componentes principais e a hierarquia de memória, base para entender desempenho.

## Teoria
- **CPU**: executa instruções. Possui **núcleos (cores)**, **clock** (GHz) e **caches** (L1, L2, L3). Ciclo básico: *buscar → decodificar → executar*.
- **RAM**: memória volátil e rápida onde ficam os programas e dados em uso. Perde o conteúdo sem energia.
- **Armazenamento**: persistente. **HDD** (disco magnético, lento) vs **SSD** (flash, bem mais rápido).
- **GPU**: milhares de núcleos simples, ótima para tarefas paralelas (gráficos, IA).

### Hierarquia de memória (do mais rápido ao mais lento)
Registradores → Cache L1/L2/L3 → RAM → SSD → HDD → Rede.
Quanto mais perto da CPU, mais rápido, menor e mais caro.

### Ordens de grandeza (aprox.)
| Acesso | Latência |
|--------|----------|
| Cache L1 | ~1 ns |
| RAM | ~100 ns |
| SSD | ~100 µs |
| HDD | ~10 ms |
| Rede (outro continente) | ~100 ms |

**Lição prática:** evitar ir ao disco ou à rede desnecessariamente é uma das maiores otimizações possíveis (cache!).

## Exercício
1. No seu computador, descubra: modelo da CPU, número de núcleos, RAM total e tipo de disco (Linux: `lscpu`, `free -h`, `lsblk`).
2. Explique por que abrir muitos programas pode deixar o PC lento (dica: RAM e swap).

## Checklist
- [ ] Diferencio RAM de armazenamento
- [ ] Sei o que são núcleos e cache
- [ ] Entendo a hierarquia de memória e por que cache existe
