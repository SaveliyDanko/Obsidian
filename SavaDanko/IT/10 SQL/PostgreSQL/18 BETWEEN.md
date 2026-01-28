Оператор `BETWEEN` проверяет, находится ли значение включительно между двумя границами.
```sql
x BETWEEN a AND b
```

###### **Синтаксис**
```sql
SELECT ...
FROM ...
WHERE выражение BETWEEN нижняя_граница AND верхняя_граница;
```

###### **С числовыми значениями**
```sql
SELECT * FROM products
WHERE price BETWEEN 100 AND 500;
```

###### **С датами**
```sql
SELECT * FROM orders
WHERE created_at BETWEEN '2024-01-01' AND '2024-01-31';
```

###### **С текстом (лексикографически)**
```sql
SELECT * FROM users
WHERE name BETWEEN 'A' AND 'F';
```
