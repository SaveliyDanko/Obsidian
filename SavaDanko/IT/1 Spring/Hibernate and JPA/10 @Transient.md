---
tags:
  - review
sr-due: 2026-03-19
sr-interval: 79
sr-ease: 250
---

---
Аннотация `@Transient` говорит JPA, что это поле не нужно сохранять в базу данных.
```java
@Entity
public class User {

    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @Transient
    private int sessionCount;  // не сохраняется в БД
}
```
