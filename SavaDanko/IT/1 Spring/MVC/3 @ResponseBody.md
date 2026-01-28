---
tags:
  - review
sr-due: 2026-01-27
sr-interval: 3
sr-ease: 250
---

---
Аннотация `@ResponseBody` в Spring используется для возврата данных в формате JSON, XML или в виде обычного текста вместо рендеринга представления (например, HTML). Она позволяет передавать объект как ответ, автоматически сериализуя его в нужный формат.
```java
@ResponseBody
@GetMapping("/hello")
public String hello() {
    return "Hello, World!";
}
```
