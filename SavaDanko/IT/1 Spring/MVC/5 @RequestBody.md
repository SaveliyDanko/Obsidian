---
tags:
  - review
sr-due: 2026-01-27
sr-interval: 3
sr-ease: 250
---

---
`@RequestBody` — это аннотация, которая указывает программе, что данные из тела входящего HTTP-запроса нужно автоматически превратить в готовый Java-объект.
```json
{
  "username": "Ivan_Java",
  "email": "ivan@example.com"
}
```

```java
@PostMapping("/register")
public String createUser(@RequestBody User user) {
    return "Пользователь сохранен!";
}
```