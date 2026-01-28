Команда `DROP` в PostgreSQL используется для удаления объектов базы данных: таблиц, представлений, индексов, схем, баз данных, пользователей, ролей, функций и др.

###### **Общий синтаксис**
```sql
DROP объект_типа [IF EXISTS] имя [CASCADE | RESTRICT];
```

###### **`DROP TABLE` — удалить таблицу**
```sql
DROP TABLE users;
```
Удаляет физическую таблицу и все её данные.

С опцией:
```sql
DROP TABLE IF EXISTS users CASCADE;
```
- `IF EXISTS` — не выбрасывает ошибку, если таблицы нет.
- `CASCADE` — автоматически удаляет зависимости (например, внешние ключи, представления).

###### **`DROP VIEW` — удалить представление**
```sql
DROP VIEW active_users;
```

###### **`DROP INDEX` — удалить индекс**
```sql
DROP INDEX idx_users_email;
```
Это не влияет на таблицу и данные, только на производительность запросов.

###### **`DROP SCHEMA` — удалить схему**
```sql
DROP SCHEMA analytics CASCADE;
```
Удаляет схему и все объекты внутри неё.

Без `CASCADE` — выбросит ошибку, если внутри есть таблицы или другие объекты.

###### **`DROP DATABASE` — удалить базу данных**
```sql
DROP DATABASE company_db;
```

Можно выполнить только вне удаляемой базы:
```bash
psql -d postgres
```

###### **`DROP ROLE / USER` — удалить пользователя или роль**
```sql
DROP ROLE analyst;
DROP USER readonly_user;
```

###### **`DROP FUNCTION` / `DROP PROCEDURE`**
```sql
DROP FUNCTION get_discount(INT);
DROP PROCEDURE sync_orders();
```
Учитывает имя и сигнатуру аргументов.

###### **`DROP TYPE`, `DROP SEQUENCE`, `DROP TRIGGER`, `DROP EXTENSION`**
```sql
DROP TYPE mood;
DROP SEQUENCE user_id_seq;
DROP TRIGGER trg_users_log ON users;
DROP EXTENSION IF EXISTS "uuid-ossp";
```
