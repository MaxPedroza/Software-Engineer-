# Aula 2 — Assistentes de código (GitHub Copilot e similares)

**Duração:** ~20 min · **Módulo 22**

## Objetivo
Usar assistentes de código de forma eficaz nos principais modos de interação.

## Teoria
Modos típicos (ex.: GitHub Copilot, Cursor, Claude Code, Gemini Code Assist):
- **Autocompletar inline**: sugere a próxima linha/bloco enquanto você digita. Ótimo para boilerplate e padrões repetitivos.
- **Chat**: perguntas sobre o código, explicação, geração de trechos, correção de erros.
- **Edição multiarquivo / modo agente**: planeja e altera vários arquivos, roda comandos e testes.
- **CLI e PRs**: explicar comandos, resumir PRs, sugerir revisões.

### O que determina a qualidade
- **Contexto**: arquivos abertos, seleção, `#file`/menções, instruções do repositório (ex.: `.github/copilot-instructions.md`).
- Nomes claros, comentários/docstrings e testes existentes guiam melhor a sugestão.
- Tarefas **pequenas e bem delimitadas** funcionam melhor que pedidos vagos.

### Boas práticas
- Você é o **responsável** pelo código: leia, entenda e teste tudo que aceitar.
- Não envie segredos nem dados pessoais; conheça a política de dados da ferramenta e da empresa.
- Use para acelerar o que já entende; para aprender, peça explicações e compare.

## Exemplo: guiando a sugestão
```python
def normalizar_cpf(cpf: str) -> str:
    """Remove pontos e traço; levanta ValueError se não tiver 11 dígitos."""
    # Com docstring clara, o assistente tende a sugerir:
    digitos = "".join(c for c in cpf if c.isdigit())
    if len(digitos) != 11:
        raise ValueError("CPF deve ter 11 dígitos")
    return digitos
```

## Exemplo: instruções do repositório
```markdown
<!-- .github/copilot-instructions.md -->
- Python 3.12, type hints obrigatórios, testes com pytest.
- Siga a estrutura em src/ e tests/; não adicione dependências sem justificar.
```

## Exercício
1. Resolva a mesma tarefa com e sem docstring/contexto e compare as sugestões.
2. Escreva um arquivo de instruções para o seu projeto e teste o efeito.

## Checklist
- [ ] Conheço os modos: inline, chat, agente
- [ ] Forneço bom contexto
- [ ] Reviso tudo que aceito
