# Aula 9 — Riscos: alucinações, segurança, licenças e ética

**Duração:** ~25 min · **Módulo 22**

## Objetivo
Identificar e mitigar os principais riscos ao usar ou construir com IA.

## Teoria
| Risco | Descrição | Mitigação |
|-------|-----------|-----------|
| **Alucinação** | Resposta plausível, porém falsa | RAG com citações, validação, testes, revisão humana |
| **Prompt injection** | Texto malicioso altera o comportamento | Separar dados de instruções, menor privilégio, filtrar saída, confirmação humana |
| **Vazamento de dados** | Envio de segredos/PII a terceiros | Mascarar dados, políticas de uso, contratos de privacidade, modelos locais |
| **Código inseguro** | Vulnerabilidades geradas | Revisão, SAST, testes |
| **Licenças/PI** | Trechos sob licenças restritivas | Filtros de duplicação, política da empresa, revisão |
| **Viés e ética** | Resultados discriminatórios | Avaliar por grupos, transparência, supervisão humana |
| **Dependência excessiva** | Perda de habilidade e de senso crítico | Revisar, entender, praticar sem IA |
| **Custo e disponibilidade** | Preços, limites, indisponibilidade | Cache, limites, fallback |

- **OWASP Top 10 para LLMs** lista riscos como prompt injection, tratamento inseguro de saída e *excessive agency*.
- **LGPD**: informe o uso de IA, minimize dados pessoais e garanta revisão humana em decisões automatizadas.
- Nunca execute a saída do modelo (SQL, shell, HTML) sem validação.

## Exemplo: guardrails simples
```python
import re

PADROES_PII = [r"\b\d{3}\.?\d{3}\.?\d{3}-?\d{2}\b", r"[\w.+-]+@[\w-]+\.[\w.]+"]

def mascarar(texto: str) -> str:
    for p in PADROES_PII:
        texto = re.sub(p, "[REMOVIDO]", texto)
    return texto

ACOES_PERMITIDAS = {"criar_tarefa", "listar_tarefas"}

def executar(acao: str, args: dict):
    if acao not in ACOES_PERMITIDAS:   # allowlist para saída do modelo
        raise PermissionError(f"ação não permitida: {acao}")
    ...
```

## Template: documento de riscos
```text
Funcionalidade: | Dados enviados ao modelo: | Fornecedor/retenção:
Risco | Probabilidade | Impacto | Mitigação | Responsável
```

## Exercício
1. Preencha o documento de riscos para o seu recurso com LLM (≥ 6 riscos).
2. Tente uma prompt injection no seu recurso e documente o resultado e a defesa.

## Checklist
- [ ] Conheço os riscos principais
- [ ] Mascaro dados sensíveis antes de enviar
- [ ] Uso allowlist e revisão humana
