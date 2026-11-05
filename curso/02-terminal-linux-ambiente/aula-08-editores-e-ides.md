# Aula 8 — Editores e IDEs (VS Code, atalhos, extensões)

**Duração:** ~20 min · **Módulo 2**

## Objetivo
Configurar o VS Code com atalhos e extensões que aumentam sua produtividade.

## Teoria
- **Editor** (VS Code, Vim, Nano): leve, extensível. **IDE** (PyCharm, IntelliJ): integrado, com refatoração e depuração profundas. VS Code fica no meio-termo via extensões.
- Recursos essenciais: terminal integrado (`` Ctrl+` ``), explorador, busca global, controle de versão, depurador, IntelliSense.

| Atalho (Win/Linux) | Ação |
|--------------------|------|
| `Ctrl+P` | abrir arquivo por nome |
| `Ctrl+Shift+P` | paleta de comandos |
| `Ctrl+Shift+F` | buscar no projeto |
| `Ctrl+D` | selecionar próxima ocorrência (multi-cursor) |
| `Alt+↑/↓` | mover linha |
| `Ctrl+/` | comentar linha |
| `F2` | renomear símbolo |
| `F5` | depurar |

- Extensões úteis: Python, Pylance, GitLens, Docker, Dev Containers, EditorConfig, Prettier/Ruff.
- Configurações em `.vscode/settings.json` (por projeto). `.editorconfig` padroniza indentação e fim de linha entre editores.
- Abrir pelo terminal: `code .`

## Exemplo
`.vscode/settings.json`:
```json
{
  "editor.formatOnSave": true,
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,
  "python.analysis.typeCheckingMode": "basic"
}
```
`.editorconfig`:
```ini
root = true
[*]
indent_style = space
indent_size = 4
end_of_line = lf
charset = utf-8
```

## Exercício
1. Instale as extensões Python e GitLens e abra a pasta do projeto com `code .`.
2. Pratique: renomeie uma variável com `F2` e edite 3 linhas ao mesmo tempo com `Ctrl+D`.
3. Crie `.editorconfig` e `.vscode/settings.json` no repositório do projeto.

## Checklist
- [ ] Uso paleta de comandos e busca global
- [ ] Tenho extensões essenciais instaladas
- [ ] Configurei `.editorconfig`
