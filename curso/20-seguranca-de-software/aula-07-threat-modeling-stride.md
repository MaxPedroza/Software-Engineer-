# Aula 7 — Threat modeling (STRIDE)

**Duração:** ~25 min · **Módulo 20**

## Objetivo
Identificar ameaças no design, antes de escrever o código.

## Teoria
Threat modeling responde quatro perguntas: **(1)** O que estamos construindo? **(2)** O que pode dar errado? **(3)** O que faremos a respeito? **(4)** Fizemos um bom trabalho?

Passos: desenhar um **DFD** (atores, processos, repositórios, fluxos, *fronteiras de confiança*) e analisar cada elemento com **STRIDE**:

| Letra | Ameaça | Propriedade violada | Mitigação |
|-------|--------|---------------------|-----------|
| S | Spoofing (falsa identidade) | Autenticidade | MFA, mTLS |
| T | Tampering (adulteração) | Integridade | Assinaturas, TLS, validação |
| R | Repudiation (negar autoria) | Não repúdio | Logs de auditoria |
| I | Information disclosure | Confidencialidade | Criptografia, controle de acesso |
| D | Denial of service | Disponibilidade | Rate limit, autoscaling |
| E | Elevation of privilege | Autorização | Menor privilégio, validação server-side |

Priorize por **risco = probabilidade × impacto**. Trate: mitigar, transferir, aceitar ou eliminar.

## Template
```text
Sistema: <nome>      Data: <dd/mm/aaaa>
DFD: <link/imagem>   Fronteiras de confiança: Internet|API / API|Banco
| ID | Elemento | STRIDE | Ameaça | Risco (A/M/B) | Mitigação | Status |
|----|----------|--------|--------|---------------|-----------|--------|
| T1 | POST /login | S | Força bruta de senhas | Alto | Rate limit + MFA | Aberto |
| T2 | Banco | I | Dump por SQLi | Alto | Queries parametrizadas | Feito |
```

## Exercício
1. Desenhe o DFD do seu projeto com ao menos 3 fronteiras de confiança.
2. Preencha o template com no mínimo 6 ameaças cobrindo letras STRIDE distintas.

## Checklist
- [ ] Desenhei um DFD com fronteiras
- [ ] Apliquei STRIDE a cada elemento
- [ ] Priorizei por risco e defini mitigações
