# Aula 5 — Estimativas e planejamento

**Duração:** ~20 min · **Módulo 21**

## Objetivo
Estimar trabalho com honestidade sobre a incerteza e planejar entregas.

## Teoria
- Estimativa **não é compromisso**: é uma previsão com incerteza (o *cone de incerteza* diminui ao longo do projeto).
- **Pontos de história**: tamanho relativo (complexidade + esforço + incerteza), em escala Fibonacci (1, 2, 3, 5, 8, 13).
- **Planning Poker**: cada pessoa vota em segredo; discutem-se divergências; revota até o consenso.
- **Velocidade**: média de pontos concluídos por sprint; use para prever (média das últimas 3–5 sprints).
- **Estimativas de três pontos**: `E = (O + 4M + P) / 6` (otimista, mais provável, pessimista).
- **Fluxo (Kanban)**: previsão por lead time e simulação de Monte Carlo — sem pontos.
- Armadilhas: viés de otimismo, ancoragem, Lei de Hofstadter, tratar velocidade como meta de produtividade, ignorar trabalho não planejado.
- Planejamento: roadmap por objetivos (Agora/Próximo/Depois), com *buffers* e riscos explícitos.

## Exemplo: previsão com velocidade
```python
velocidades = [18, 21, 16, 20]          # últimas sprints
media = sum(velocidades) / len(velocidades)
backlog = 95                            # pontos restantes
sprints = -(-backlog // media)          # arredonda para cima
print(f"~{sprints:.0f} sprints (min {-(-backlog // max(velocidades)):.0f}, "
      f"max {-(-backlog // min(velocidades)):.0f})")
```

## Exercício
1. Estime 5 histórias do seu backlog em pontos, usando uma história pequena como referência.
2. Calcule a faixa de entrega (otimista/provável/pessimista) para 60 pontos com velocidades [12, 15, 10, 14].
3. Aplique a estimativa de três pontos a uma tarefa e compare com seu palpite inicial.

## Checklist
- [ ] Sei por que estimativa ≠ compromisso
- [ ] Uso estimativa relativa e velocidade
- [ ] Comunico previsões como faixas
