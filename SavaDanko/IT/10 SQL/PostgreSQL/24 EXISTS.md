В PostgreSQL оператор `EXISTS` используется для проверки наличия строк, возвращаемых подзапросом. Это булевый предикат, который возвращает:
- `TRUE`, если подзапрос вернул хотя бы одну строку
- `FALSE`, если не вернул ни одной строки
    
###### **Синтаксис**
```sql
SELECT ...
FROM ...
WHERE EXISTS (подзапрос);
```

###### **Пользователи с заказами**
```sql
SELECT * FROM users u
WHERE EXISTS (
  SELECT 1 FROM orders o
  WHERE o.user_id = u.id
);
```
Вернёт только тех пользователей, у которых есть хотя бы один заказ.

###### **Пользователи без заказов (через `NOT EXISTS`)**
```sql
SELECT * FROM users u
WHERE NOT EXISTS (
  SELECT 1 FROM orders o
  WHERE o.user_id = u.id
);
```
Найдёт всех пользователей, **у которых нет заказов**.

###### **Сложный подзапрос**
```sql
SELECT * FROM products p
WHERE EXISTS (
  SELECT 1 FROM reviews r
  WHERE r.product_id = p.id AND r.rating >= 4
);
```
Продукты, у которых **есть хорошие отзывы**.

###### **`EXISTS` без таблиц (технический приём)**
```sql
SELECT EXISTS (
  SELECT 1 FROM users WHERE email = 'test@example.com'
);
```
Возвращает `true` или `false` — часто используется в `IF EXISTS`-проверках в процедурах или условиях.
