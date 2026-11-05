# Aula 8 — Entrevistas técnicas e de system design

**Duração:** ~25 min · **Módulo 23**

## Objetivo
Preparar-se para entrevistas de código e de design de sistemas com método.

## Teoria
### Entrevista de código
1. **Entenda**: reformule o problema, pergunte sobre entradas, limites e casos de borda.
2. **Exemplo**: resolva um caso pequeno à mão.
3. **Abordagem**: proponha força bruta e depois otimize; diga a complexidade (Big-O).
4. **Codifique** falando em voz alta, com nomes claros.
5. **Teste** com exemplos e casos de borda (vazio, um elemento, duplicados).
- Prática: resolver problemas por padrão (hash map, dois ponteiros, janela deslizante, BFS/DFS, DP).

### System design (45 min)
| Etapa | Tempo | O que fazer |
|-------|-------|-------------|
| Requisitos | 5–8 min | Funcionais, não funcionais (latência, disponibilidade), escala |
| Estimativas | 5 min | Usuários, QPS, armazenamento |
| API e modelo de dados | 5–8 min | Endpoints e tabelas principais |
| Arquitetura | 15 min | Cliente, LB, serviços, banco, cache, filas, CDN |
| Gargalos | 10 min | Escala, replicação, falhas, trade-offs |

- Sempre **explicite trade-offs** (consistência × disponibilidade, custo × latência).

### Exemplo: estimativa
`10M usuários/dia × 5 acessos = 50M/dia ≈ 580 req/s em média; pico ×3 ≈ 1.800 req/s`.

## Exercício
1. Resolva 3 problemas de nível fácil/médio falando o raciocínio em voz alta (grave-se).
2. Desenhe o design de um encurtador de URLs: requisitos, API, modelo, geração de ID, cache, escala.
3. Faça uma simulação com um colega e peça feedback.

## Checklist
- [ ] Sigo um método em problemas de código
- [ ] Conduzo system design em etapas
- [ ] Explicito trade-offs e complexidade
