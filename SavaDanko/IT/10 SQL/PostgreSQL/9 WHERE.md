###### **Общий синтаксис**
```sql
SELECT столбцы
FROM таблица
WHERE условие;
```

###### **Простое сравнение**
```sql
SELECT * FROM users
WHERE age > 18;
```

###### **Сравнение с текстом**
```sql
SELECT * FROM products
WHERE name = 'iPhone 14';
```
Регистр в PostgreSQL учитывается, если не использовать `ILIKE`.

###### **Несколько условий (`AND`, `OR`)**
```sql
SELECT * FROM users
WHERE age > 18 AND country = 'Germany';
```

###### **Операторы `IN`, `NOT IN`**
```sql
SELECT * FROM orders
WHERE status IN ('shipped', 'processing');
```

###### **Диапазон `BETWEEN`**
```sql
SELECT * FROM payments
WHERE amount BETWEEN 100 AND 500;
```
Эквивалент: `amount >= 100 AND amount <= 500`.

###### **Маска `LIKE` и `ILIKE`**
```sql
SELECT * FROM users
WHERE name LIKE 'A%';     -- с заглавной A
```

```sql
SELECT * FROM users
WHERE name ILIKE '%ivan%';  -- нечувствительно к регистру
```
`%` — любой набор символов, `_` — один символ.

###### **Проверка на `NULL`**
```sql
SELECT * FROM users
WHERE email IS NULL;

SELECT * FROM users
WHERE phone IS NOT NULL;
```
`email = NULL` не работает — сравнение с `NULL` делается через `IS`.
