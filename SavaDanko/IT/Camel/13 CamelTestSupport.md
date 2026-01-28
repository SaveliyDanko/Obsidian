---
tags:
  - review
sr-due: 2026-02-12
sr-interval: 41
sr-ease: 250
---

---
`CamelTestSupport` — это базовый класс в Apache Camel (модуль `camel-test`) для удобного написания юнит-тестов маршрутов Camel. Он создаёт минимальный Camel-контекст, автоматически запускает его, даёт удобные методы для тестирования маршрутов и работы с mock-endpoint’ами.

Проще говоря, это готовая инфраструктура для тестирования Camel-маршрутов, чтобы не поднимать вручную CamelContext, ProducerTemplate, компоненты и т.п.

###### **ProducerTemplate уже готов**
Можно сразу отправлять сообщения в маршруты:
```java
template.sendBody("direct:start", "Hello");
```

###### **Поддерживает Mock endpoints**
Mock-endpoint — это специальный компонент Camel для проверки, что маршрут отправил правильные данные.

В тесте:
```java
MockEndpoint mock = getMockEndpoint("mock:result");
mock.expectedBodiesReceived("Hello");
```

###### **Удобное тестирование маршрутов**
```java
public class MyRouteTest extends CamelTestSupport {

    @Override
    protected RouteBuilder createRouteBuilder() {
        return new MyRoute();
    }

    @Test
    public void testMyRoute() throws Exception {
        getMockEndpoint("mock:result").expectedBodiesReceived("test");

        template.sendBody("direct:start", "test");

        assertMockEndpointsSatisfied();
    }
}
```

###### **Основные методы, которые предоставляет `CamelTestSupport`**

| Метод                            | Для чего                                          |
| -------------------------------- | ------------------------------------------------- |
| `createRouteBuilder()`           | возвращаешь `RouteBuilder`, который ты тестируешь |
| `context`                        | доступ к CamelContext                             |
| `template`                       | готовый `ProducerTemplate`                        |
| `getMockEndpoint("mock:...")`    | получить mock-endpoint                            |
| `assertMockEndpointsSatisfied()` | проверить ожидания mock-endpoint’ов               |
| `adviceWith()`                   | модифицировать маршрут прямо перед тестом         |
