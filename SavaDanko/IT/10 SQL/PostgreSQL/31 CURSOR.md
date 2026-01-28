Курсоры в SQL — это механизм пошагового (строчного) перебора результатов запроса, особенно полезный, когда необходимо выполнить операцию над каждой строкой выборки по отдельности.

###### **Зачем нужны курсоры**
По умолчанию SQL-операторы работают с множествами данных. Но иногда тебе нужно:
- обрабатывать строки по одной
- использовать условную логику или сложные вычисления над каждой строкой
- выполнять итерации, которых невозможно достичь чисто декларативными средствами SQL.
Именно в таких случаях и применяются **курсорные циклы**.

###### **Как работает курсор**
1. Выполняется SQL-запрос → результат сохраняется как контекст выборки.
2. Курсор открывается.
3. Каждая строка извлекается по одной (в цикле).
4. После завершения — курсор закрывается.
    

###### **Пример: курсор в PostgreSQL (PL/pgSQL)**
Допустим, у нас есть таблица:
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name TEXT,
  active BOOLEAN DEFAULT true
);
```
Теперь мы хотим отключить всех пользователей по определённому правилу, используя курсор:
```sql
DO $$
DECLARE
  user_record RECORD;
  user_cursor CURSOR FOR SELECT id, name FROM users WHERE active = true;
BEGIN
  OPEN user_cursor;

  LOOP
    FETCH user_cursor INTO user_record;
    EXIT WHEN NOT FOUND;

    -- Выполняем какую-то логику
    RAISE NOTICE 'Отключаем пользователя: %', user_record.name;

    UPDATE users SET active = false WHERE id = user_record.id;
  END LOOP;

  CLOSE user_cursor;
END $$;
```

###### **Упрощённый вариант с `FOR ... IN` (авто-курсор)**
PostgreSQL позволяет не создавать курсор явно, а использовать неявный курсор через `FOR ... IN`:
```sql
DO $$
DECLARE
  user_record RECORD;
BEGIN
  FOR user_record IN SELECT id, name FROM users WHERE active = true
  LOOP
    -- Аналогичная логика
    RAISE NOTICE 'Отключаем пользователя: %', user_record.name;

    UPDATE users SET active = false WHERE id = user_record.id;
  END LOOP;
END $$;
```
Этот способ проще, безопаснее и предпочтительнее в большинстве случаев.
