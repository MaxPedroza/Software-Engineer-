# Aula 1 — Definição de escopo, requisitos e backlog

**Duração:** ~30 min · **Módulo 24 — Etapa 1**

## Objetivo
Definir o problema, o escopo do MVP, os requisitos e um backlog priorizado para o projeto final.

## Passo a passo
1. **Escolha o produto** (ex.: plataforma de tarefas, e-commerce, agendamento). Escreva a visão em 2 frases.
2. **Personas e jornadas**: 2 personas e a jornada principal de cada uma.
3. **Requisitos funcionais** como histórias de usuário: *Como [persona], quero [ação], para [valor]*.
4. **Requisitos não funcionais** mensuráveis: p95 < 300 ms, disponibilidade 99,5%, LGPD, cobertura ≥ 80%.
5. **Escopo**: liste o que está *dentro* e *fora* do MVP.
6. **Backlog priorizado** com MoSCoW (Must/Should/Could/Won't) e critérios de aceite (Dado/Quando/Então).
7. **Riscos** e plano de mitigação; marcos semanais.

### Template de história
```text
US-01 Criar tarefa (Must)
Como usuário, quero criar uma tarefa com título e prazo, para organizar meu dia.
Aceite: Dado que estou logado, Quando envio título válido, Então a tarefa aparece na lista.
```

## Entregáveis
- `docs/00-visao-e-escopo.md` (visão, personas, dentro/fora do escopo)
- Backlog no GitHub Projects com 15+ issues rotuladas e priorizadas
- Lista de requisitos não funcionais com métricas

## Critérios de aceite
- [ ] MVP cabe em ~4 semanas e tem pelo menos 8 histórias Must
- [ ] Toda história tem critério de aceite testável
- [ ] Requisitos não funcionais têm número e forma de medir
- [ ] Repositório criado com README inicial e licença
