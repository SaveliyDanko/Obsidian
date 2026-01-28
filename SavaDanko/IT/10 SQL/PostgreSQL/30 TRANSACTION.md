В PostgreSQL транзакции — это атомарные группы SQL-операций, которые выполняются всё сразу или не выполняются вообще, обеспечивая ACID-гарантии (атомарность, согласованность, изолированность и долговечность).

###### **Синтаксис транзакций в PostgreSQL**
```sql
BEGIN;        -- или START TRANSACTION;
-- SQL-операции
COMMIT;       -- сохранить изменения
```
или
```sql
ROLLBACK;     -- откатить изменения при ошибке
```

###### **Пример 1. Простая транзакция: перевод денег**
Допустим, у нас есть таблица:
```sql
CREATE TABLE accounts (
  id SERIAL PRIMARY KEY,
  name TEXT,
  balance NUMERIC
);
```

Мы хотим перевести 100 единиц с аккаунта 1 на аккаунт 2:
```sql
BEGIN;

UPDATE accounts SET balance = balance - 100 WHERE id = 1;
UPDATE accounts SET balance = balance + 100 WHERE id = 2;

COMMIT;
```
Если что-то пойдёт не так (например, недостаточно денег), мы можем откатить:
```sql
ROLLBACK;
```

###### **Пример 2. Обработка ошибки через транзакцию**
```sql
BEGIN;

UPDATE accounts SET balance = balance - 100 WHERE id = 1;

-- Проверка
DO $$
BEGIN
  IF (SELECT balance FROM accounts WHERE id = 1) < 0 THEN
    RAISE EXCEPTION 'Недостаточно средств';
  END IF;
END $$;

UPDATE accounts SET balance = balance + 100 WHERE id = 2;

COMMIT;
```
Если `RAISE EXCEPTION` сработает → PostgreSQL выполнит `ROLLBACK` автоматически.

###### Пример 3. Использование `SAVEPOINT` для частичного отката
```sql
BEGIN;

INSERT INTO orders (customer_id, total) VALUES (42, 250);
SAVEPOINT after_order;

-- допустим, проблема со вставкой позиции заказа
INSERT INTO order_items (order_id, product_id, qty)
VALUES (9999, 12, 2);  -- ошибка: order_id 9999 не существует

ROLLBACK TO SAVEPOINT after_order;

-- продолжаем с другого шага:
INSERT INTO log (message) VALUES ('Order created, items skipped');

COMMIT;
```

###### **Уровни изоляции транзакций в PostgreSQL**
PostgreSQL поддерживает:
```sql
SET TRANSACTION ISOLATION LEVEL READ COMMITTED;      -- по умолчанию
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```
**`READ COMMITTED`**: каждая команда видит актуальные зафиксированные данные  
**`REPEATABLE READ`**: вся транзакция работает в рамках одного "снимка"  
**`SERIALIZABLE`**: транзакции выполняются как будто последовательно
