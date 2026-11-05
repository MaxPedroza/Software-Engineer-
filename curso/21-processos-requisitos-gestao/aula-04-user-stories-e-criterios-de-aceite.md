# Aula 4 — User stories e critérios de aceite

**Duração:** ~25 min · **Módulo 21**

## Objetivo
Escrever histórias de usuário de qualidade com critérios de aceite testáveis.

## Teoria
### User story
Formato: **Como** <persona>, **quero** <capacidade>, **para** <benefício>.

### INVEST
Uma boa história é **I**ndependente, **N**egociável, **V**aliosa, **E**stimável, **S**mall (pequena), **T**estável.

### Critérios de aceite (Gherkin / BDD)
Formato **Dado–Quando–Então**, que pode virar teste automatizado.

### Épicos e fatiamento
Divida épicos em histórias verticais (que atravessam UI, API e banco) em vez de camadas técnicas. Evite "fazer o backend" como história.

## Template
```text
ID: US-012      Prioridade: Alta     Estimativa: 3 pts
Como  usuária cadastrada
Quero filtrar minhas tarefas por status
Para  focar no que ainda está pendente

Critérios de aceite:
  Cenário: filtrar por pendentes
    Dado que tenho 3 tarefas, 2 pendentes e 1 concluída
    Quando seleciono o filtro "Pendentes"
    Então vejo apenas as 2 tarefas pendentes

  Cenário: nenhum resultado
    Dado que não tenho tarefas pendentes
    Quando seleciono o filtro "Pendentes"
    Então vejo a mensagem "Nada pendente 🎉"

Fora do escopo: filtros combinados
```

## Do critério ao teste
```python
def test_filtrar_pendentes():
    tarefas = [Tarefa("a", False), Tarefa("b", False), Tarefa("c", True)]
    assert len(filtrar(tarefas, status="pendente")) == 2
```

## Exercício
1. Escreva 5 histórias para o seu backlog, cada uma com ≥ 2 cenários.
2. Aplique INVEST: qual história é grande demais? Divida-a.

## Checklist
- [ ] Uso o formato Como/Quero/Para
- [ ] Critérios em Dado/Quando/Então
- [ ] Histórias pequenas e testáveis
