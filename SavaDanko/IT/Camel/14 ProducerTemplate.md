---
tags:
  - review
sr-due: 2026-02-02
sr-interval: 34
sr-ease: 250
---

---
`ProducerTemplate` — это ключевой интерфейс в Apache Camel, который позволяет отправлять сообщения в любой endpoint Camel из вашего кода.

Ты указываешь URI (например, `direct:start`, `kafka:topic`, `file:outbox`, `seda:queue`), а Camel сам подбирает нужный компонент и доставляет сообщение.

###### **Зачем нужен ProducerTemplate**
Он даёт удобный API, чтобы:
- запускать маршруты вручную (например, тесты)
- отправлять данные в Camel из обычного Java-кода
- получать ответ от маршрута (если это request-response)
- работать с процессингом как с методами

###### **Основные операции ProducerTemplate**
Camel предоставляет много удобных методов:
`sendBody(endpointUri, body)`
Отправить только тело:
```java
template.sendBody("direct:start", "Hello Camel");
```

`sendBodyAndHeader(endpointUri, body, header, value)`
Отправить тело + заголовок:
```java
template.sendBodyAndHeader(
    "direct:process", 
    "data",
    "type", 
    "json"
);
```

`requestBody(endpointUri, body)`
Отправить запрос и получить ответ (InOut):
```java
String result = template.requestBody("direct:calc", 5, String.class);
```

`send(...)`
Полный доступ к Exchange:
```java
template.send("direct:start", exchange -> {
    exchange.getIn().setBody("ABC");
    exchange.getIn().setHeader("id", 10);
});
```