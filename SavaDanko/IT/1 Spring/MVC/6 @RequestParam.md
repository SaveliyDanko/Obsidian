---
tags:
  - review
sr-due: 2026-01-27
sr-interval: 3
sr-ease: 250
---

---
Аннотация `@RequestParam` в Spring используется для извлечения параметров из строки запроса (query parameters) или из формы в HTTP-запросах. Она позволяет легко получать данные из URL или тела запроса, поддерживая различные типы данных и параметры по умолчанию.

```java
@GetMapping("/greet")
public String greet(@RequestParam String name) {
    return "Hello, " + name + "!";
}
```

###### Необязательный параметр с значением по умолчанию:
```java
@RequestParam(defaultValue = "Guest")
```

###### Несколько параметров:
```java
@RequestParam String name, @RequestParam int age
```

###### Множественные значения (список):
```java
@RequestParam List<String> tags) {
```
