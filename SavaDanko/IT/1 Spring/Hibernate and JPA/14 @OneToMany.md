---
tags:
  - review
sr-due: 2026-05-10
sr-interval: 111
sr-ease: 250
---

---
`@OneToMany` — Один ко многим
Один объект A связан со множеством объектов B.
Это обратная сторона `@ManyToOne`.

###### **Как это выглядит вместе**
```java
@Entity
public class University {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @OneToMany(mappedBy = "university", cascade = CascadeType.ALL)
    private List<Student> students = new ArrayList<>();
}

@Entity
public class Student {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @ManyToOne
    @JoinColumn(name = "university_id")
    private University university;
}
```
В таблицах:
- `university.id` — первичный ключ
- `student.university_id` — внешний ключ
    

###### **Атрибуты, которые часто используются**

| Атрибут         | Применяется к          | Назначение                                                        |
| --------------- | ---------------------- | ----------------------------------------------------------------- |
| `mappedBy`      | @OneToMany / @OneToOne | Указывает обратную сторону связи                                  |
| `cascade`       | Все связи              | Определяет, распространяются ли операции (persist, remove и т.д.) |
| `fetch`         | Все связи              | Определяет стратегию загрузки (`LAZY` или `EAGER`)                |
| `orphanRemoval` | @OneToMany / @OneToOne | Автоматически удаляет «осиротевшие» записи                        |
