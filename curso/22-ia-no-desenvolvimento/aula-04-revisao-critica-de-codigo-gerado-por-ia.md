# Aula 4 — Revisão crítica de código gerado por IA

**Duração:** ~25 min · **Módulo 22**

## Objetivo
Revisar código de IA com o mesmo rigor (ou mais) que código humano.

## Teoria
Código gerado parece correto mesmo quando não é. Problemas frequentes:
- **APIs/pacotes inexistentes** (alucinação) ou versões obsoletas; pacotes com nome inventado podem ser alvo de *slopsquatting*.
- **Falhas de segurança**: SQL concatenado, segredos no código, validação ausente, criptografia fraca.
- **Casos-limite ignorados**: vazio, `None`, fuso horário, concorrência, grandes volumes.
- **Complexidade desnecessária**, duplicação, testes que só confirmam a implementação.
- **Licenças**: trechos que lembram código sob licença restritiva.

### Checklist de revisão
1. Entendi cada linha? Se não, não aceite.
2. Dependências existem, são mantidas e necessárias?
3. Segurança: entrada validada, queries parametrizadas, sem segredos?
4. Casos-limite e erros tratados?
5. Testes cobrem comportamento (não só o caminho feliz) e **falham** se o código quebrar?
6. Segue as convenções do projeto? Rodou linter, tipos e CI?

## Exemplo: o que a IA entregou e o que revisar
```python
# Gerado
def buscar_usuario(conn, nome):
    return conn.execute(f"SELECT * FROM usuarios WHERE nome = '{nome}'").fetchall()
```
Problemas: SQL injection, `SELECT *`, sem limite. Corrigido:
```python
def buscar_usuario(conn, nome: str):
    cur = conn.execute(
        "SELECT id, nome, email FROM usuarios WHERE nome = ? LIMIT 50", (nome,)
    )
    return cur.fetchall()
```
Teste que prova a correção:
```python
def test_nao_vulneravel_a_injecao(conn):
    assert buscar_usuario(conn, "' OR '1'='1") == []
```

## Exercício
1. Peça a uma IA uma função de upload de arquivos e revise com o checklist; liste ≥ 3 problemas.
2. Verifique se cada dependência sugerida existe no registro oficial (PyPI/npm).

## Checklist
- [ ] Nunca aceito código que não entendo
- [ ] Reviso segurança e casos-limite
- [ ] Valido dependências e rodo os testes
