---
tags:
  - review
sr-due: 2026-04-19
sr-interval: 84
sr-ease: 250
---

---
[[14 Жизненный цикл Bean]]

---
```java
@Component
public class ConnectionManager {

    @PostConstruct
    public void init() {
        System.out.println("🚀 Init: Подключение к базе...");
    }

    @PreDestroy
    public void destroy() {
        System.out.println("💥 Destroy: Закрытие подключения...");
    }
}
```
Аннотации:
- `@PostConstruct` — вызывается после создания бина и внедрения зависимостей
- `@PreDestroy` — вызывается перед удалением бина (только для singleton-бинов!)
