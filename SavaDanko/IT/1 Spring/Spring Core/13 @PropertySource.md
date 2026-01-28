---
tags:
  - review
sr-due: 2026-02-23
sr-interval: 31
sr-ease: 250
---

---
#### Как добавить файл свойств вручную
```java
@Configuration
@PropertySource("classpath:application.properties")
public class AppConfig {}
```
В Spring Boot это **не требуется** — всё подключается автоматически.
