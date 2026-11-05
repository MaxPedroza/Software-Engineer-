# Aula 1 — Conceitos de bancos de dados e SGBDs

**Duração:** ~20 min · **Módulo 10**

## Objetivo
Entender o que é um banco de dados, um SGBD e as diferenças entre bancos relacionais e NoSQL.

## Teoria
- **Banco de dados**: coleção organizada de dados persistentes. **SGBD**: software que o gerencia (PostgreSQL, MySQL, SQLite, SQL Server, Oracle).
- Um SGBD oferece: persistência, consultas, controle de concorrência, integridade, segurança e recuperação de falhas.
- **Modelo relacional**: dados em **tabelas** (relações) com **linhas** (registros) e **colunas** (atributos), ligadas por **chaves**: primária (PK) identifica a linha; estrangeira (FK) referencia outra tabela.
- **SQL** é a linguagem declarativa padrão: DDL (`CREATE`, `ALTER`), DML (`SELECT`, `INSERT`...), DCL (`GRANT`), TCL (`COMMIT`).
- **NoSQL**: documentos (MongoDB), chave-valor (Redis), colunar (Cassandra), grafos (Neo4j). Útil quando o esquema varia muito ou a escala horizontal é prioridade.
- Bancos relacionais são a escolha padrão para dados estruturados com integridade e transações.

## Exemplo (PostgreSQL)
```bash
docker run --name pg -e POSTGRES_PASSWORD=dev -p 5432:5432 -d postgres:16
psql -h localhost -U postgres
```
```sql
CREATE TABLE usuarios (
  id    SERIAL PRIMARY KEY,
  nome  TEXT NOT NULL,
  email TEXT NOT NULL UNIQUE
);

INSERT INTO usuarios (nome, email) VALUES ('Ana', 'ana@exemplo.com');
SELECT * FROM usuarios;
```

## Exercício
1. Suba o PostgreSQL (Docker ou instalação local) e conecte com `psql`.
2. Crie a tabela `usuarios` e insira 3 registros; use `\dt` e `\d usuarios`.
3. Cite um caso em que NoSQL seria preferível e justifique.

## Checklist
- [ ] Diferencio banco de dados e SGBD
- [ ] Explico tabela, linha, PK e FK
- [ ] Tenho um PostgreSQL funcionando
