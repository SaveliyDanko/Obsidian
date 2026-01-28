В PostgreSQL оператор `CASE` — это мощный инструмент для условной логики в SQL-запросах. Он работает как конструкция `if-else` в языках программирования: позволяет выбирать значение в зависимости от условий, прямо внутри `SELECT`, `WHERE`, `ORDER BY`, `GROUP BY` и других выражений.

###### **Общий синтаксис `CASE`**
```sql
CASE
  WHEN условие1 THEN результат1
  WHEN условие2 THEN результат2
  ...
  ELSE результат_по_умолчанию
END
```
`ELSE` — необязателен, но рекомендуется: если ни одно условие не выполнено, и `ELSE` не указан — результатом будет `NULL`.

###### **В SELECT — на лету вычисляем поле**
```sql
SELECT name,
       CASE
         WHEN age < 18 THEN 'Minor'
         WHEN age BETWEEN 18 AND 65 THEN 'Adult'
         ELSE 'Senior'
       END AS age_group
FROM users;
```
Создаёт колонку `age_group` по возрасту.

###### **В ORDER BY — кастомная сортировка**
```sql
SELECT * FROM tasks
ORDER BY 
  CASE status
    WHEN 'urgent' THEN 1
    WHEN 'normal' THEN 2
    ELSE 3
  END;
```
Сначала идут `urgent`, потом `normal`, потом остальные.

###### **В WHERE — условная фильтрация**
```sql
SELECT * FROM orders
WHERE 
  CASE 
    WHEN total > 1000 THEN TRUE
    WHEN customer_id = 1 THEN TRUE
    ELSE FALSE
  END;
```
Покажет заказы >1000 и все от клиента №1.
