---
tags:
  - review
sr-due: 2026-02-20
sr-interval: 63
sr-ease: 250
---

---
###### **Principal**
- Представляет текущего пользователя — “кто вошёл в систему”.
- Содержит идентификатор личности, обычно `username`.

###### **Authentication**
- Более “богатый” объект, чем `Principal`.
- Хранит всю информацию о входе:
    - `principal` — пользователь (`UserDetails`);
    - `authorities` — роли/права;
    - `credentials` — пароль или токен;
    - `details` — доп. данные запроса.

![[Pasted image 20251109001750.png]]
