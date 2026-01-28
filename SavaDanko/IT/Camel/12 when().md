---
tags:
  - review
sr-due: 2026-03-13
sr-interval: 68
sr-ease: 250
---

---
###### **when()**
- Определяет условие, при котором сообщение пойдёт по определённой ветке.
- Внутри него указывают выражение, predicate или язык Camel (Simple, JSONPath и т.п.).
- После выполнения первого подходящего `when()` остальные игнорируются.
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
