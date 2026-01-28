###### **LIMIT — ограничение количества строк**
```sql
SELECT * FROM users
ORDER BY created_at DESC
LIMIT 10;
```

###### **`OFFSET` — пропуск строк**
Пропускает указанное число строк до начала результата.
```sql
SELECT * FROM users
ORDER BY created_at DESC
OFFSET 20 LIMIT 10;
```