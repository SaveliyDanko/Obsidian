---
tags:
  - review
sr-due: 2026-03-22
sr-interval: 77
sr-ease: 250
---

---
**Endpoints в Apache Camel** — это точки входа и выхода маршрута.  
Они определяют, откуда Camel получает сообщения и куда их отправляет.

###### **Примеры Endpoints**
```java
from("file:input")          // endpoint чтения из папки
.to("file:output");         // endpoint записи в папку
```

```java
from("kafka:orders")        // чтение из Kafka
.to("http://service/api");  // отправка HTTP‐запроса
```