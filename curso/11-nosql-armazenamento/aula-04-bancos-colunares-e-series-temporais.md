# Aula 4 — Bancos colunares e séries temporais

**Duração:** ~20 min · **Módulo 11**

## Objetivo
Entender armazenamento por colunas, *wide-column* e bancos de séries temporais, e quando usá-los.

## Teoria
- **Orientado a linhas** (PostgreSQL, MySQL): bom para OLTP, lê o registro inteiro.
- **Orientado a colunas** (ClickHouse, BigQuery, Parquet): guarda cada coluna junta; ótimo para OLAP — agregações sobre poucas colunas de bilhões de linhas, com forte compressão.
- **Wide-column** (Cassandra, HBase): partições por chave, escrita muito rápida e escalável, consultas planejadas a partir da chave de partição (sem joins).
- **Séries temporais** (TimescaleDB, InfluxDB, Prometheus): dados com timestamp, escritos em ordem, consultados por janelas de tempo, com retenção e *downsampling*.

| Caso | Escolha |
|------|---------|
| Relatórios analíticos | Colunar |
| Escrita massiva distribuída | Cassandra |
| Métricas e sensores | Série temporal |

## Exemplo
Consulta típica em série temporal (TimescaleDB, SQL):
```sql
CREATE TABLE leituras (ts timestamptz NOT NULL, sensor int, temp double precision);
SELECT create_hypertable('leituras', 'ts');

SELECT time_bucket('5 minutes', ts) AS janela, sensor, avg(temp)
FROM leituras
WHERE ts > now() - interval '1 hour'
GROUP BY janela, sensor ORDER BY janela;
```
Em Cassandra (CQL), a chave define o acesso:
```sql
CREATE TABLE tarefas_por_usuario (
  usuario_id uuid, criada_em timestamp, titulo text,
  PRIMARY KEY (usuario_id, criada_em)) WITH CLUSTERING ORDER BY (criada_em DESC);
```

## Exercício
1. Por que somar uma coluna é mais rápido em formato colunar?
2. Que banco usaria para guardar o consumo de CPU de 500 servidores por 90 dias? Que política de retenção?

## Checklist
- [ ] Diferencio linha de coluna
- [ ] Sei o que é série temporal e retenção
- [ ] Sei quando usar Cassandra
