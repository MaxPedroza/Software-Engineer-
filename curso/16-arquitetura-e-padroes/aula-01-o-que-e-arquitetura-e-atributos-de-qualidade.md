# Aula 1 — O que é arquitetura e atributos de qualidade

**Duração:** ~20 min · **Módulo 16**

## Objetivo
Compreender o papel da arquitetura de software e usar atributos de qualidade para guiar decisões.

## Teoria
- **Arquitetura** é o conjunto de decisões significativas e difíceis de mudar sobre a estrutura do sistema: componentes, responsabilidades, relações e tecnologias.
- Não é só diagrama: é o resultado de **trade-offs** ("tudo tem custo").
- **Atributos de qualidade** (requisitos não funcionais) guiam a arquitetura:
  - **Desempenho**, **escalabilidade**, **disponibilidade**, **confiabilidade**
  - **Segurança**, **manutenibilidade**, **testabilidade**, **observabilidade**, **custo**
- Atributos conflitam: mais segurança pode reduzir desempenho; mais escalabilidade aumenta a complexidade.
- Transforme em **cenários mensuráveis**: "Com 1.000 req/s, p95 < 300 ms".
- **Princípios**: separação de responsabilidades, baixo acoplamento, alta coesão, SOLID, KISS/YAGNI.
- **Arquiteto**: decide com base em contexto e evidências; evite *over-engineering*. "Comece simples e evolua."
- **Dívida técnica**: atalhos que cobram juros futuros; gerencie-a conscientemente.

## Exemplo: priorizar atributos em código
```python
# Cenário de qualidade escrito como teste (fitness function)
import time

def test_listagem_responde_em_menos_de_300ms(client):
    inicio = time.perf_counter()
    resposta = client.get("/tarefas")
    duracao_ms = (time.perf_counter() - inicio) * 1000

    assert resposta.status_code == 200
    assert duracao_ms < 300
```
```text
Cenário: Disponibilidade
Fonte: usuário · Estímulo: falha de uma instância da API
Ambiente: produção · Resposta: balanceador redireciona o tráfego
Medida: indisponibilidade < 30 s, 99,9% ao mês
```

## Exercício
1. Liste os 3 atributos de qualidade mais importantes do sistema de tarefas e justifique a ordem.
2. Escreva um cenário mensurável para cada um (formato acima).
3. Dê um exemplo de conflito entre dois atributos e a decisão que você tomaria.

## Checklist
- [ ] Defino arquitetura como decisões e trade-offs
- [ ] Cito atributos de qualidade e seus conflitos
- [ ] Escrevo cenários de qualidade mensuráveis
