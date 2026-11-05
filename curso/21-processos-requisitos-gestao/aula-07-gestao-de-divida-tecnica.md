# Aula 7 — Gestão de dívida técnica

**Duração:** ~20 min · **Módulo 21**

## Objetivo
Identificar, registrar, priorizar e pagar dívida técnica de forma sustentável.

## Teoria
**Dívida técnica** (Ward Cunningham): atalhos de design/código que aceleram hoje e cobram "juros" depois, na forma de lentidão e bugs.

### Quadrante de Fowler
| | Deliberada | Inadvertida |
|--|-----------|-------------|
| **Prudente** | "Entregamos agora e refatoramos depois" | "Agora sabemos como deveria ter sido" |
| **Imprudente** | "Não temos tempo para design" | "O que é arquitetura em camadas?" |

### Fontes
Código duplicado, falta de testes, dependências defasadas, documentação ausente, arquitetura que não acompanhou o domínio.

### Como gerir
1. **Tornar visível**: registrar itens no backlog com a etiqueta `tech-debt`.
2. **Priorizar** por *juros* (quanto atrapalha) × *custo* de pagar × risco.
3. **Reservar capacidade** (ex.: 15–20% de cada sprint) e aplicar a *regra do escoteiro*: deixe o código melhor do que encontrou.
4. **Medir**: análise estática (SonarQube), churn × complexidade, tempo de build, bugs recorrentes.
5. Preferir refatoração **incremental** a "reescrever tudo".

## Template: registro de dívida
```text
ID: TD-007    Área: módulo de pagamentos
Descrição: cálculo de desconto duplicado em 4 lugares
Impacto (juros): cada regra nova leva 4x mais tempo; 2 bugs/trimestre
Custo de pagar: 3 dias     Risco se adiado: Médio
Proposta: extrair `calcular_desconto()` + testes de caracterização
Prioridade: P2
```

## Exercício
1. Levante 5 dívidas técnicas do seu projeto usando o template.
2. Ordene-as por juros × custo e escolha 1 para a próxima sprint.

## Checklist
- [ ] Defino dívida técnica e seus juros
- [ ] Mantenho registro priorizado
- [ ] Reservo capacidade para pagá-la
