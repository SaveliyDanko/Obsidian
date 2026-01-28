---
tags:
  - review
sr-due: 2026-02-15
sr-interval: 73
sr-ease: 250
---

---
`@Id` указывает, что поле является **первичным ключом** в таблице базы данных.
- Поле с аннотацией `@Id` обязательно должно присутствовать в каждой сущности.
- В сочетании с `@GeneratedValue` можно автоматически генерировать значения.
```java
@Entity
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
}
```

| Стратегия генерации       | Описание                                  |
| ------------------------- | ----------------------------------------- |
| `GenerationType.AUTO`     | Выбор Hibernate (в зависимости от БД)     |
| `GenerationType.IDENTITY` | Генерация с автоинкрементом               |
| `GenerationType.SEQUENCE` | Использует последовательность (sequence)  |
| `GenerationType.TABLE`    | Хранит идентификаторы в отдельной таблице |
