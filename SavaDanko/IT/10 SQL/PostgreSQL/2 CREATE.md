В PostgreSQL команда `CREATE` используется для создания объектов в базе данных: таблиц, схем, индексов, представлений, ролей, баз данных, функций и многого другого. Это часть DDL (Data Definition Language) — языка определения данных.

###### **Общий синтаксис**
```sql
CREATE <тип_объекта> имя [опции...];
```

###### **`CREATE TABLE` — создать таблицу**
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT UNIQUE,
    registered_at TIMESTAMP DEFAULT now()
);
```

###### **`CREATE SCHEMA` — создать схему**
```sql
CREATE SCHEMA accounting;
```
Создаёт пространство имён (логическую группу объектов).

###### **`CREATE DATABASE` — создать базу данных**
```sql
CREATE DATABASE company_db;
```
Создаёт отдельную базу, с собственными схемами и таблицами.

###### **`CREATE INDEX` — создать индекс**
```sql
CREATE INDEX idx_users_email ON users (email);
```
Повышает производительность выборки по `email`.

###### **`CREATE VIEW` — создать представление**
```sql
CREATE VIEW active_users AS
SELECT * FROM users WHERE active = true;
```
Виртуальная таблица, не хранящая данные.

###### **`CREATE FUNCTION` — создать функцию**
```sql
CREATE FUNCTION get_discount(age INT) RETURNS INT AS $$
BEGIN
  RETURN CASE WHEN age > 60 THEN 20 ELSE 0 END;
END;
$$ LANGUAGE plpgsql;
```
Хранимая процедура/функция на языке `plpgsql` или SQL.

###### **`CREATE ROLE / USER` — создать роль или пользователя**
```sql
CREATE ROLE analyst WITH LOGIN PASSWORD 'secret';
```

###### **`CREATE TYPE` — пользовательский тип**
```sql
CREATE TYPE mood AS ENUM ('happy', 'sad', 'neutral');
```
