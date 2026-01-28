---
tags:
  - review
sr-due: 2026-01-29
sr-interval: 1
sr-ease: 230
---

---
###### **DML (Data Manipulation Language)**
Манипулирование данными — это работа с конкретными строками в таблицах: добавление, изменение, удаление, выборка.

###### **Что входит в манипулирование:**

| Операция | Пример SQL                                            | Назначение                 |
| -------- | ----------------------------------------------------- | -------------------------- |
| `SELECT` | `SELECT * FROM users WHERE age > 30;`                 | Получение данных из таблиц |
| `INSERT` | `INSERT INTO users (name, age) VALUES ('Alice', 25);` | Добавление новых строк     |
| `UPDATE` | `UPDATE users SET age = 26 WHERE name = 'Alice';`     | Изменение данных           |
| `DELETE` | `DELETE FROM users WHERE age < 18;`                   | Удаление данных            |
    