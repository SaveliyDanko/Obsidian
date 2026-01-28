В PostgreSQL оператор `UNION` используется для объединения результатов двух (или более) SQL-запросов в один набор строк.
- Объединяет строки из двух запросов.
- Возвращает одно результирующее множество.
- Имена и количество столбцов в каждом запросе должны совпадать по порядку и типу.
- По умолчанию удаляет дубликаты — это отличие от `UNION ALL`.
    

###### **Синтаксис**
```sql
SELECT ... FROM таблица1
UNION
SELECT ... FROM таблица2;
```

###### **Объединение двух таблиц**
```sql
SELECT name FROM students
UNION
SELECT name FROM teachers;
```
Результат: имена студентов и учителей, без повторов.

###### **С `ORDER BY`**
Если хочешь отсортировать итог:
```sql
SELECT name FROM students
UNION
SELECT name FROM teachers
ORDER BY name;
```
Весь `ORDER BY` применяется к объединённому результату.

###### **С `ALL`: оставить дубликаты**
```sql
SELECT name FROM students
UNION ALL
SELECT name FROM teachers;
```
Включит все строки, включая дубли.

###### **Разные типы → явное приведение**
```sql
SELECT id::TEXT AS val FROM users
UNION
SELECT email FROM contacts;
```
Приводим `id` к `TEXT`, чтобы типы совпадали.
