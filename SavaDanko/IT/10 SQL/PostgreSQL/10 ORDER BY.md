Команда `ORDER BY` в PostgreSQL используется для сортировки результата SQL-запроса по одному или нескольким столбцам (или выражениям), в возрастающем (`ASC`) или убывающем (`DESC`) порядке.

###### **Синтаксис**
```sql
SELECT столбцы
FROM таблица
ORDER BY выражение_1 [ASC | DESC] [NULLS FIRST | LAST],
         выражение_2 [ASC | DESC] ...;
```


###### **Сортировка по одному столбцу**
```sql
SELECT name, age
FROM users
ORDER BY age;
```
По умолчанию — `ASC` (по возрастанию).

###### **Убывающая сортировка (`DESC`)**
```sql
SELECT name, age
FROM users
ORDER BY age DESC;
```


###### **Сортировка по нескольким столбцам**
```sql
SELECT name, age
FROM users
ORDER BY country ASC, age DESC;
```
Сначала сортирует по стране (по алфавиту), а внутри страны — по убыванию возраста.

###### **Сортировка по порядковому номеру столбца**
```sql
SELECT name, age
FROM users
ORDER BY 2 DESC;
```
`2` означает второй столбец (`age`), не рекомендуется — хуже читается.

###### **Сортировка по вычисляемому выражению**
```sql
SELECT name, salary, salary * 12 AS yearly_salary
FROM employees
ORDER BY yearly_salary DESC;
```
Или:
```sql
ORDER BY salary * 12 DESC
```

###### **Сортировка с `NULLS FIRST / LAST`**
```sql
SELECT name, last_login
FROM users
ORDER BY last_login DESC NULLS LAST;
```
Указывает, куда помещать `NULL`-значения (по умолчанию: `NULLS FIRST` при `ASC`, `NULLS LAST` при `DESC`).

###### **Сортировка по выражению с функцией**
```sql
SELECT name, LOWER(name) AS lower_name
FROM users
ORDER BY LOWER(name);
```

###### **Сортировка с `DISTINCT ON` (уникальный случай PostgreSQL)**
```sql
SELECT DISTINCT ON (user_id) user_id, created_at, status
FROM orders
ORDER BY user_id, created_at DESC;
```
Оставляет первую строку по `user_id`, при этом `ORDER BY` определяет какая именно первая.