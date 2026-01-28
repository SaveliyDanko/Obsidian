###### **`JOIN`**
Сравнивает строки из двух таблиц по условию связи (обычно по внешнему ключу) и объединяет их в одну строку результата.

###### **`INNER JOIN` — пересечение**
Возвращает только те строки, у которых есть совпадения в обеих таблицах.
```sql
SELECT u.name, o.total
FROM users u
INNER JOIN orders o ON u.id = o.user_id;
```
Пользователи, у которых есть заказы.

###### **`LEFT JOIN`**
Возвращает все строки из левой таблицы, даже если нет совпадений в правой.  
Если совпадений нет — поля правой таблицы будут **`NULL`**.
```sql
SELECT u.name, o.total
FROM users u
LEFT JOIN orders o ON u.id = o.user_id;
```

###### **`RIGHT JOIN`**
Аналогично `LEFT JOIN`, но теперь все строки из правой таблицы попадают в результат.
```sql
SELECT u.name, o.total
FROM users u
RIGHT JOIN orders o ON u.id = o.user_id;
```

###### **`FULL JOIN`**
Возвращает:
- все строки, у которых есть совпадения,
- все строки из левой таблицы без совпадений (`NULL` справа),
- все строки из правой таблицы без совпадений (`NULL` слева).
```sql
SELECT u.name, o.total
FROM users u
FULL JOIN orders o ON u.id = o.user_id;
```