---
tags:
  - review
sr-due: 2026-03-21
sr-interval: 81
sr-ease: 250
---

---
Аннотация `@Enumerated` указывает, как хранить enum-поля в базе данных:
- как число (ordinal)
- или как строку (string)
Если не указать `@Enumerated`, JPA по умолчанию сохранит enum как число (ordinal), то есть индекс константы в перечислении:

| Enum  | Индекс |
| ----- | ------ |
| ADMIN | 0      |
| USER  | 1      |

В таблице окажется, например:

| id  | role |
| --- | ---- |
| 1   | 0    |
| 2   | 1    |

###### **Пример с `@Enumerated(EnumType.STRING)`**
```java
@Entity
public class Person {
    @Id
    @GeneratedValue
    private Long id;

    @Enumerated(EnumType.STRING)
    private Role role;
}
```
Теперь в таблице хранится текстовое имя константы, а не число:

|id|role|
|---|---|
|1|ADMIN|
|2|USER|
