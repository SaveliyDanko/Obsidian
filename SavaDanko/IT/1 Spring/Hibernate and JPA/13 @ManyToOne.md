---
tags:
  - review
sr-due: 2026-02-15
sr-interval: 35
sr-ease: 230
---

---
`@ManyToOne` — «Многие к одному»
Много объектов A принадлежат одному объекту B.  

Пример:
```java
@Entity
public class Student {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    @ManyToOne
    private University university;
}
```

```java
@Entity
public class University {
    @Id
    @GeneratedValue
    private Long id;

    private String name;
    
    @OneToMany(mappedBy = "university", cascade = CascadeType.ALL)
    private List<Student> students;
}
```
