В PostgreSQL `VIEW` (представление) — это виртуальная таблица, основанная на результате SQL-запроса. Представление не хранит данные самостоятельно, а лишь сохраняет SQL-логику, которая выполняется при обращении к view.

###### **Синтаксис**
```sql
CREATE VIEW имя_view AS
SELECT ... FROM ... WHERE ...;
```

Пример:
```sql
CREATE VIEW active_users AS
SELECT id, name, email
FROM users
WHERE is_active = TRUE;
```

Теперь ты можешь писать:
```sql
SELECT * FROM active_users;
```
и PostgreSQL выполнит исходный `SELECT` внутри `VIEW`.

###### **Сложный join в `VIEW`**
```sql
CREATE VIEW user_order_stats AS
SELECT u.id AS user_id, u.name,
       COUNT(o.id) AS orders_count,
       SUM(o.total) AS total_spent
FROM users u
LEFT JOIN orders o ON o.user_id = u.id
GROUP BY u.id, u.name;
```

Теперь ты можешь делать:
```sql
SELECT * FROM user_order_stats WHERE total_spent > 1000;
```
