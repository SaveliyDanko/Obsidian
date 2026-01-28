
###### **Общий синтаксис `SELECT`**
```sql
SELECT [DISTINCT] [колонки или выражения]
FROM источник_данных
[WHERE условие]
[GROUP BY ...]
[HAVING ...]
[ORDER BY ...]
[LIMIT ... OFFSET ...];
```

###### **Простой пример:**
```sql
SELECT name, age
FROM users
WHERE age > 18
ORDER BY age DESC
LIMIT 10;
```

###### **`SELECT` + выражения**
```sql
SELECT id, name, age + 1 AS next_year_age
FROM users;
```
Можно использовать выражения, функции, арифметику, алиасы.

###### **`DISTINCT` / `DISTINCT ON`**
Удаляет дубликаты:
```sql
SELECT DISTINCT country FROM users;
```

###### **`FROM` + JOIN**
Соединение таблиц:
```sql
SELECT u.name, o.total
FROM users u
JOIN orders o ON u.id = o.user_id;
```

###### **`WHERE` — фильтрация строк**
```sql
WHERE age > 18 AND active = true
```
Также можно использовать:
- `IN`, `NOT IN`
- `BETWEEN`
- `LIKE`, `ILIKE`
- `IS NULL`, `IS NOT NULL`

###### **`GROUP BY` + агрегаты**
```sql
SELECT country, COUNT(*) AS users_count
FROM users
GROUP BY country;
```
Агрегатные функции: `COUNT()`, `SUM()`, `AVG()`, `MAX()`, `MIN()`

###### **`HAVING` — фильтрация групп**
```sql
HAVING COUNT(*) > 10
```
Применяется после группировки.

###### **`ORDER BY` — сортировка**
```sql
ORDER BY created_at DESC, id ASC
```

###### **`LIMIT` и `OFFSET`**
Пагинация:
```sql
LIMIT 10 OFFSET 20
```
Выдаст 10 строк, начиная с 21-й.
