###### **`COUNT()` — количество строк**
```sql
SELECT COUNT(*) FROM orders;
```
Количество всех строк (даже с `NULL`).
```sql
SELECT COUNT(email) FROM users;
```
Количество не-NULL значений в столбце `email`.
