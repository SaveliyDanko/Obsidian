В PostgreSQL (и в SQL в целом) `CROSS JOIN` — это тип соединения таблиц, при котором каждая строка из первой таблицы соединяется с каждой строкой из второй таблицы. Это называется декартово произведение (Cartesian Product).

###### **Синтаксис**
```sql
SELECT *
FROM таблица1
CROSS JOIN таблица2;
```

###### **Пример**
Таблица `colors`

| color |
| ----- |
| red   |
| green |

Таблица `sizes`

| size |
| ---- |
| S    |
| M    |
| L    |

Запрос:
```sql
SELECT *
FROM colors
CROSS JOIN sizes;
```

Результат:

| color | size |
| ----- | ---- |
| red   | S    |
| red   | M    |
| red   | L    |
| green | S    |
| green | M    |
| green | L    |
