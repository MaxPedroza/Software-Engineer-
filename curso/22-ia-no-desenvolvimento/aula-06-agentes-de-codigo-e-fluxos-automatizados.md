# Aula 6 — Agentes de código e fluxos automatizados

**Duração:** ~25 min · **Módulo 22**

## Objetivo
Entender como agentes funcionam e como delegar tarefas a eles com segurança.

## Teoria
Um **agente** é um LLM em **laço** com **ferramentas**: observa → decide → age (ler arquivo, rodar teste, editar, buscar) → observa o resultado → repete até concluir.

- Componentes: modelo, instruções (prompt de sistema), **ferramentas** (function calling), memória/contexto, critério de parada.
- **MCP** (Model Context Protocol): padrão aberto para expor ferramentas e dados a agentes.
- Exemplos: modo agente do Copilot/VS Code, Copilot CLI, agente de código em nuvem que abre PRs a partir de issues.

### Boas práticas de delegação
- Tarefas **bem especificadas** com critérios de aceite e testes existentes.
- **Menor privilégio**: permissões e tokens mínimos; ambiente isolado (sandbox/container).
- **Humano no circuito**: aprovação de comandos destrutivos; todo código passa por PR e CI.
- Limite de passos/custos; logs e rastreabilidade.
- Risco: *prompt injection* em issues, páginas ou arquivos lidos pelo agente.

## Exemplo: laço de agente mínimo
```python
import json
from openai import OpenAI  # pip install openai

client = OpenAI()
ferramentas = [{"type": "function", "function": {
    "name": "rodar_testes", "description": "Executa pytest e retorna a saída",
    "parameters": {"type": "object", "properties": {}}}}]

msgs = [{"role": "user", "content": "Faça os testes passarem."}]
for _ in range(5):  # limite de passos
    r = client.chat.completions.create(model="gpt-4o-mini", messages=msgs, tools=ferramentas)
    m = r.choices[0].message
    msgs.append(m)
    if not m.tool_calls:
        print(m.content); break
    for call in m.tool_calls:
        saida = executar_ferramenta(call.function.name)  # sua implementação, com sandbox
        msgs.append({"role": "tool", "tool_call_id": call.id, "content": saida})
```

## Exercício
1. Abra uma issue clara no seu repositório e delegue a um agente; revise o PR com o checklist da aula 4.
2. Liste 3 ações que exigiriam aprovação humana no seu fluxo.

## Checklist
- [ ] Descrevo o laço do agente
- [ ] Aplico menor privilégio e limites
- [ ] Todo resultado passa por revisão e CI
