---
tags:
  - review
sr-due: 2026-03-24
sr-interval: 79
sr-ease: 250
---

---
**Processor в Apache Camel** — это компонент, который позволяет выполнять произвольную логику обработки сообщения в маршруте.

###### **Что делает Processor**
Он получает Exchange и может:
- изменить body
- добавить/изменить headers
- установить properties
- выполнить валидацию
- вызвать внешнюю логику
- генерировать новые данные

###### **Пример Processor**
```java
@Component
public class MyProcessor implements Processor {
    @Override
    public void process(Exchange exchange) {
        String body = exchange.getMessage().getBody(String.class);
        exchange.getMessage().setBody(body.toUpperCase());
    }
}
```

Использование в маршруте:
```java
from("file:input")
    .process(new MyProcessor())
    .to("file:output");
```

###### **Inline Processor (лямбда)**
```java
.process(exchange -> {
    String name = exchange.getMessage().getBody(String.class);
    exchange.getMessage().setBody("Hello " + name);
})
```
