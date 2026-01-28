---
tags:
  - review
sr-due: 2026-01-27
sr-interval: 3
sr-ease: 250
---

---
Аннотация `@RequestMapping` используется в Spring для связывания HTTP-запросов с методами контроллера. Она позволяет гибко настраивать маршруты и поддерживает различные методы HTTP (GET, POST, PUT, DELETE и т.д.).
```java
@RequestMapping(value = "/path", method = RequestMethod.GET)
public String handlerMethod() {
    return "response";
}
```
Можно использовать на уровне класса или на уровне метода.

| Аннотация      | HTTP-метод |
| -------------- | ---------- |
| @GetMapping    | GET        |
| @PostMapping   | POST       |
| @PutMapping    | PUT        |
| @DeleteMapping | DELETE     |

###### **Атрибуты аннотации @RequestMapping:**
`value` - URL-маршрут
`method` - HTTP-метод (GET, POST, PUT, DELETE и др.)

