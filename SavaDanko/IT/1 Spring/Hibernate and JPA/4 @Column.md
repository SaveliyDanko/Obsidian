---
tags:
  - review
sr-due: 2026-02-14
sr-interval: 72
sr-ease: 250
---

---
`@Column` используется для настройки маппинга поля класса на столбец базы данных, определяет параметры столбца в базе данных (имя, длину, уникальность).

| Атрибут    | Назначение                             |
| ---------- | -------------------------------------- |
| `name`     | Имя столбца в базе данных.             |
| `nullable` | Разрешает или запрещает значение NULL. |
| `unique`   | Задает уникальность столбца.           |
| `length`   | Определяет максимальную длину строки.  |

```java
@Entity
public class Product {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "product_name", length = 100, nullable = false)
    private String name;

    @Column(unique = true, nullable = true)
    private String sku;
}
```