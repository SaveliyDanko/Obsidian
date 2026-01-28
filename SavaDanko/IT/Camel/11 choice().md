---
tags:
  - review
sr-due: 2026-03-17
sr-interval: 72
sr-ease: 250
---

---
###### **choice()**
- Аналог оператора **switch / if-else** в Camel-маршрутах.
- Позволяет направлять сообщения по разным путям в зависимости от условий.
- Используется внутри _Content-Based Router_ паттерна.
- Всегда открывает блок ветвления.
```java
from("direct:start")
    .choice()
        .when(simple("${body} contains 'error'"))
            .to("log:error")
        .when(simple("${body} contains 'warn'"))
            .to("log:warn")
        .otherwise()
            .to("log:info");
```



