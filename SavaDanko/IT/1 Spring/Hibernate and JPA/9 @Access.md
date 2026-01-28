---
tags:
  - review
sr-due: 2026-03-29
sr-interval: 86
sr-ease: 250
---

---
Аннотация `@Access` управляет тем, каким образом JPA получает доступ к данным класса — через поля (Field Access) или через геттеры/сеттеры (Property Access).

По умолчанию:
```java
@Access(AccessType.FIELD)
```
→ JPA читает и пишет данные напрямую в поля (минуя геттеры/сеттеры).

```java
@Access(AccessType.PROPERTY)
```
→ JPA работает через методы доступа (get/set).

```java
@Entity
@Access(AccessType.FIELD)
public class Book {

    @Id
    private Long id;

    private String title;

    @Access(AccessType.PROPERTY)
    private String author;

    public String getAuthor() {
        return author == null ? "Неизвестен" : author;
    }
    public void setAuthor(String author) { this.author = author; }
}

```