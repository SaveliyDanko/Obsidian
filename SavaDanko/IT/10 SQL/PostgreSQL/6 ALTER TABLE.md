Команда `ALTER TABLE` в PostgreSQL используется для изменения структуры существующей таблицы: добавления, удаления или изменения столбцов, ключей, ограничений, параметров хранения и других аспектов.

###### **Общий синтаксис**
```sql
ALTER TABLE имя_таблицы действие_изменения;
```
PostgreSQL позволяет выполнять несколько изменений за раз, разделяя их запятыми:
```sql
ALTER TABLE users
  ADD COLUMN email TEXT,
  DROP COLUMN age,
  RENAME TO app_users;
```

###### **`ADD COLUMN` — добавить столбец**
```sql
ALTER TABLE users
ADD COLUMN phone TEXT;
```

###### **`DROP COLUMN` — удалить столбец**
```sql
ALTER TABLE users
DROP COLUMN age;
```

###### **`RENAME COLUMN` — переименовать столбец**
```sql
ALTER TABLE users
RENAME COLUMN email TO email_address;
```


###### **`ALTER COLUMN` — изменить столбец**
Изменить тип:
```sql
ALTER TABLE users
ALTER COLUMN age TYPE BIGINT;
```
> PostgreSQL попробует **преобразовать значения** автоматически (возможно, потребуется `USING`):
```sql
ALTER TABLE users
ALTER COLUMN birthdate TYPE TIMESTAMP USING birthdate::timestamp;
```

Задать или убрать `DEFAULT`:
```sql
ALTER TABLE users
ALTER COLUMN registered_at SET DEFAULT now();

ALTER TABLE users
ALTER COLUMN registered_at DROP DEFAULT;
```

Задать или убрать `NOT NULL`:
```sql
ALTER TABLE users
ALTER COLUMN name SET NOT NULL;

ALTER TABLE users
ALTER COLUMN name DROP NOT NULL;
```

###### **Ограничения (`CONSTRAINTS`)**
Добавить `CHECK`:
```sql
ALTER TABLE users
ADD CONSTRAINT check_age CHECK (age >= 0);
```

Добавить внешний ключ:
```sql
ALTER TABLE orders
ADD CONSTRAINT fk_user FOREIGN KEY (user_id) REFERENCES users(id);
```

Удалить ограничение:
```sql
ALTER TABLE users
DROP CONSTRAINT check_age;
```

###### **`RENAME TO` — переименовать таблицу**
```sql
ALTER TABLE users
RENAME TO customers;
```

###### **Изменить владельца таблицы**
```sql
ALTER TABLE users
OWNER TO new_owner;
```

###### **SET SCHEMA — переместить таблицу в другую схему**
```sql
ALTER TABLE users SET SCHEMA analytics;
```
