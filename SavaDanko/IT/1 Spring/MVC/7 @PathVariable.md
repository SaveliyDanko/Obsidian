---
tags:
  - review
sr-due: 2026-04-12
sr-interval: 78
sr-ease: 250
---

---
Аннотация `@PathVariable` в Spring используется для извлечения значений из части URI (путь запроса). Она позволяет передавать параметры в методы контроллера через путь URL.
```java
@GetMapping("/users/{id}")
public String getUser(@PathVariable("id") String id) {
    return "User ID: " + id;
}
```

```
http://localhost:8080/users/42
```