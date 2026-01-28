```sql
DELETE FROM table_name
WHERE condition;
```

###### Удаление всех данных из таблицы:
```sql
DELETE FROM employees;
```

Если нужно удалить все данные без сохранения истории, лучше использовать команду `TRUNCATE`, так как она быстрее и менее ресурсоёмкая:
```sql
TRUNCATE TABLE employees;
```
