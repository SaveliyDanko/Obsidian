---
tags:
  - review
sr-due: 2026-02-04
sr-interval: 36
sr-ease: 250
---

---
`MockEndpoint` — это специальный компонент Apache Camel, предназначенный для тестирования маршрутов.  

###### **Пример использования**
Маршрут:
```java
from("direct:start")
    .transform(simple("${body.toUpperCase()}"))
    .to("mock:result");
```

Тест:
```java
@Test
public void testRoute() throws Exception {
    MockEndpoint mock = getMockEndpoint("mock:result");

    mock.expectedBodiesReceived("HELLO");

    template.sendBody("direct:start", "hello");

    mock.assertIsSatisfied();
}
```
Здесь `mock:result` ничего не делает — он просто проверяет, что в него пришло `"HELLO"`.