# Demo presto

1. Start `docker-compose`
2. Add new table to postgres
3. Add message like `kafka-message-sample.json` to kafka topic `clicks` (create topic before publish message)
4. Start presto-cli ([download](https://prestodb.io/docs/current/installation/cli.html))
5. Query data from Postgres & Kafka

More connectors at https://prestodb.io/docs/current/connector.html

## Postgres query

```
presto> SELECT id, name FROM postgresql.public.clients WHERE id = 2;
 id |  name  
----+--------
  2 | name 2 
(1 row)

Query 20210808_201945_00011_wc4bg, FINISHED, 1 node
Splits: 17 total, 17 done (100.00%)
144ms [1 rows, 0B] [6 rows/s, 0B/s]
```

## Kafka query

```
presto> SELECT name, max(phone) FROM kafka.default.clicks WHERE name is not null GROUP BY name;
   name   | _col1 
----------+-------
 myNameIs | 0001  
(1 row)

Query 20210808_201913_00009_wc4bg, FINISHED, 1 node
Splits: 49 total, 49 done (100.00%)
105ms [3 rows, 87B] [28 rows/s, 826B/s]

```
