---
tags:
  - review
sr-due: 2026-01-30
sr-interval: 28
sr-ease: 250
---

---
`Closeable` — это источник или приёмник данных, который может быть закрыт. Метод `close` вызывается для освобождения ресурсов, удерживаемых объектом (например, открытых файлов).
```java
public interface Closeable extends AutoCloseable {
    public void close() throws IOException;
}
```

###### **close**
```java
public void close() throws IOException;
```
Закрывает данный поток и освобождает все связанные с ним системные ресурсы. Если поток уже закрыт, повторный вызов этого метода не оказывает никакого эффекта.