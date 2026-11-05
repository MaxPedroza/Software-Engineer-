# Aula 3 — Levantamento e análise de requisitos

**Duração:** ~20 min · **Módulo 21**

## Objetivo
Descobrir, classificar e validar requisitos com stakeholders.

## Teoria
- **Requisito funcional (RF)**: o que o sistema faz ("o usuário pode redefinir a senha").
- **Requisito não funcional (RNF)**: como ele se comporta — desempenho, segurança, disponibilidade, usabilidade, conformidade (LGPD).
- **Restrições**: prazo, orçamento, tecnologia imposta.

### Técnicas de levantamento
Entrevistas, workshops, observação (*shadowing*), questionários, análise de documentos e sistemas existentes, protótipos, análise de dados de uso.

### Boas práticas
- Identifique **stakeholders** (usuários, cliente, operação, jurídico).
- Pergunte "por quê?" para chegar à necessidade real, não à solução pedida.
- Um bom requisito é **claro, verificável, atômico, rastreável e priorizado**.
- Evite termos vagos: "rápido", "fácil", "amigável".
- Valide com protótipos e mantenha uma matriz de rastreabilidade.

### Exemplo
| ID | Tipo | Requisito | Verificação |
|----|------|-----------|-------------|
| RF-01 | Funcional | O usuário pode filtrar tarefas por status | Teste de aceitação |
| RNF-01 | Desempenho | A listagem responde em ≤ 300 ms p95 com 10 mil tarefas | Teste de carga |
| RNF-02 | Segurança | Senhas armazenadas com Argon2id | Revisão de código |

## Template: roteiro de entrevista
```text
Contexto: quem é você / qual seu fluxo hoje?
Dor: qual a maior dificuldade? com que frequência?
Objetivo: como seria o sucesso? como medir?
Restrições: prazos, regras, integrações?
```

## Exercício
1. Entreviste (ou simule) um usuário do seu sistema e liste 5 RF e 3 RNF mensuráveis.
2. Reescreva "o sistema deve ser rápido" como requisito verificável.

## Checklist
- [ ] Diferencio RF e RNF
- [ ] Escrevo requisitos verificáveis
- [ ] Identifiquei os stakeholders
