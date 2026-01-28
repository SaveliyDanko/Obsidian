---
tags:
  - review
sr-due: 2026-03-05
sr-interval: 76
sr-ease: 250
---

---
В JPA у каждой связи (`@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`) есть параметр `fetch type`, который определяет как будут загружаться связанные сущности из базы данных:

| Тип загрузки      | Аннотация        | Поведение                                                                                            |
| ----------------- | ---------------- | ---------------------------------------------------------------------------------------------------- |
| `FetchType.EAGER` | `EAGER` (жадная) | Данные загружаются сразу вместе с основной сущностью, даже если ты их не используешь.                |
| `FetchType.LAZY`  | `LAZY` (ленивая) | Данные загружаются только по необходимости (при первом обращении к связанной коллекции или объекту). |

###### **Пример**
```java
@Entity
public class Author {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    // Один автор может иметь много книг
    @OneToMany(mappedBy = "author", fetch = FetchType.LAZY)
    private List<Book> books = new ArrayList<>();
}

@Entity
public class Book {
    @Id
    @GeneratedValue
    private Long id;

    private String title;

    @ManyToOne(fetch = FetchType.EAGER)
    private Author author;
}
```

---
###### **Поведение в работе**
`EAGER`
Когда ты делаешь:
```java
Author a = entityManager.find(Author.class, 1L);
```
Hibernate сразу выполнит JOIN-запрос и загрузит все книги автора, даже если ты их не просил:
```sql
SELECT a.*, b.* FROM author a
LEFT JOIN book b ON b.author_id = a.id
WHERE a.id = 1;
```


`LAZY`
Когда ты делаешь:
```java
Author a = entityManager.find(Author.class, 1L);
```
Hibernate загрузит только автора, без книг:
```sql
SELECT * FROM author WHERE id = 1;
```
А когда ты впервые обратился к `a.getBooks()`, произойдёт второй запрос:
```sql
SELECT * FROM book WHERE author_id = 1;
```
Минус: может привести к ошибке `LazyInitializationException`, если коллекцию вызвать вне контекста сессии (например, после закрытия `EntityManager`)

---
###### **Стратегии по умолчанию**

| Тип связи     | FetchType по умолчанию |
| ------------- | ---------------------- |
| `@OneToOne`   | `EAGER`                |
| `@ManyToOne`  | `EAGER`                |
| `@OneToMany`  | `LAZY`                 |
| `@ManyToMany` | `LAZY`                 |

Поэтому для коллекций обычно ничего не нужно писать — они уже ленивые.
