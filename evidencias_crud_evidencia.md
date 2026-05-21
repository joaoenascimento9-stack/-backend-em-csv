# Evidências - INSERT, UPDATE e DELETE no banco db_em

## Identificação

Nome: João Emanuel Custódio Nascimento
Turma: 3°A EM
Data: 21/05/2026

---

# 1. SELECT final - Leituras do dia 2026-04-04

Execute no DBeaver:

```sql
SELECT *
FROM leituras
WHERE timestamp >= '2026-04-04'
  AND timestamp < '2026-04-05'
ORDER BY timestamp ASC;
```

Cole abaixo a saída obtida:

```text
 id | station_id      | timestamp                     | temperature_c | humidity_pct
----+-----------------+-------------------------------+---------------+--------------
  4 | EM-ARACATUBA-01 | 2026-04-04 08:00:00.000 -0300 |          23.4 |         76.2
  5 | EM-ARACATUBA-01 | 2026-04-04 09:00:00.000 -0300 |          25.2 |           72
  6 | EM-ARACATUBA-01 | 2026-04-04 10:00:00.000 -0300 |          25.9 |         70.5

3 row(s) fetched
```

---

# 2. SELECT final - Conferência do UPDATE

Execute no DBeaver:

```sql
SELECT *
FROM leituras
WHERE station_id = 'EM-ARACATUBA-01'
  AND timestamp = '2026-04-04 09:00:00';
```

Cole abaixo a saída obtida:

```text
 id | station_id      | timestamp                     | temperature_c | humidity_pct
----+-----------------+-------------------------------+---------------+--------------
  5 | EM-ARACATUBA-01 | 2026-04-04 09:00:00.000 -0300 |          25.2 |           72

1 row(s) fetched
```

---

# 3. SELECT final - Conferência do DELETE

Execute no DBeaver:

```sql
SELECT *
FROM leituras
WHERE station_id = 'EM-ARACATUBA-01'
  AND timestamp = '2026-04-04 11:00:00';
```

Cole abaixo a saída obtida:

```text
 id | station_id | timestamp | temperature_c | humidity_pct
----+------------+-----------+---------------+--------------

No data - 0 row(s) fetched
```

Se o DELETE foi feito corretamente, esse SELECT não deverá retornar registros.

---

# 4. SELECT final - Todas as leituras ordenadas

Execute no DBeaver:

```sql
SELECT *
FROM leituras
ORDER BY id ASC;
```

Cole abaixo a saída obtida:

```text
 id | station_id      | timestamp                     | temperature_c | humidity_pct
----+-----------------+-------------------------------+---------------+--------------
  1 | EM-ARACATUBA-01 | 2026-04-01 08:00:00.000 -0300 |          24.5 |         72.1
  2 | EM-ARACATUBA-01 | 2026-04-01 09:00:00.000 -0300 |          25.8 |         69.4
  3 | EM-ARACATUBA-01 | 2026-04-01 10:00:00.000 -0300 |          27.2 |         65.8
  4 | EM-ARACATUBA-01 | 2026-04-04 08:00:00.000 -0300 |          23.4 |         76.2
  5 | EM-ARACATUBA-01 | 2026-04-04 09:00:00.000 -0300 |          25.2 |           72
  6 | EM-ARACATUBA-01 | 2026-04-04 10:00:00.000 -0300 |          25.9 |         70.5

6 row(s) fetched
```

---

# 5. Teste pela API

Acesse no navegador:

```text
http://localhost:3000/api/leituras/data/2026-04-04
```

Cole abaixo o resultado retornado pela API:

```json
{
  "dataPesquisada": "2026-04-04",
  "total": 3,
  "leituras": [
    {
      "id": 4,
      "station_id": "EM-ARACATUBA-01",
      "timestamp": "2026-04-04T11:00:00.000Z",
      "temperature_c": 23.4,
      "humidity_pct": 76.2
    },
    {
      "id": 5,
      "station_id": "EM-ARACATUBA-01",
      "timestamp": "2026-04-04T12:00:00.000Z",
      "temperature_c": 25.2,
      "humidity_pct": 72
    },
    {
      "id": 6,
      "station_id": "EM-ARACATUBA-01",
      "timestamp": "2026-04-04T13:00:00.000Z",
      "temperature_c": 25.9,
      "humidity_pct": 70.5
    }
  ]
}
```

---

# 6. Conclusão

Explique com suas palavras a diferença entre INSERT, UPDATE e DELETE.

Resposta:

```text
O INSERT é usado para adicionar novos registros em uma tabela. Por exemplo, quando uma estação
meteorológica registra uma nova leitura de temperatura e umidade, usamos o INSERT para salvar
esse dado no banco.

O UPDATE é usado para alterar um registro que já existe na tabela. Se uma leitura foi salva
com um valor errado de temperatura, usamos o UPDATE com WHERE para corrigir apenas aquele
registro específico, sem mexer nos outros.

O DELETE é usado para excluir um registro da tabela. Se uma leitura foi inserida por engano,
usamos o DELETE com WHERE para remover somente aquele dado. É importante sempre usar o WHERE
no UPDATE e no DELETE, caso contrário todos os registros da tabela seriam alterados ou
apagados de uma vez.
```