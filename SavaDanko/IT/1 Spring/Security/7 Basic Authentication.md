---
tags:
  - review
sr-due: 2026-02-27
sr-interval: 65
sr-ease: 250
---

---
**Basic Authentication** — это стандартный способ передачи логина и пароля в заголовке HTTP-запроса.

Идея: клиент при каждом запросе к защищённому ресурсу прикладывает свои учётные данные — имя пользователя и пароль — в заголовке `Authorization`.

###### **Как это работает**
Клиент хочет получить доступ к защищённому ресурсу:
```
GET /api/profile HTTP/1.1
Host: example.com
```

Сервер отвечает, что доступ запрещён без авторизации:
```
HTTP/1.1 401 Unauthorized
WWW-Authenticate: Basic realm="User Visible Realm"
```

Клиент повторяет запрос, добавляя заголовок `Authorization`:
```
Authorization: Basic am9obmRvZTpwYXNzd29yZA==
```
Здесь строка после `Basic` — это base64-кодированная пара `username:password`.

Пример:
```
"john_doe:password" → "am9obmRvZTpwYXNzd29yZA=="
```

###### **На стороне сервера**
Сервер:
1. Получает заголовок `Authorization`
2. Декодирует значение Base64 → получает логин и пароль
3. Сверяет их с базой пользователей (например, через `UserDetailsService`)
4. Если всё верно — создаёт `Authentication` и помещает его в `SecurityContext`.