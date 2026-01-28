---
tags:
  - review
sr-due: 2026-04-02
sr-interval: 88
sr-ease: 250
---

---
`@OneToOne` — Один к одному
Один объект A связан ровно с одним объектом B, и наоборот.

Пример:
```java
@Entity
public class Person {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @OneToOne
    private Passport passport;
}
```

```java
@Entity
public class Passport {
    @Id
    @GeneratedValue
    private Long id;

    private String number;
}
```