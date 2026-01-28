---
tags:
  - review
sr-due: 2026-02-03
sr-interval: 35
sr-ease: 250
---

---
**AggregationStrategy** — это интерфейс, который определяет, как объединять несколько сообщений (Exchange), когда вы работаете с:
- `split()`
- `aggregate()`
- `multicast()`
- `recipientList()`
- `pollEnrich/enrich()`
    
Camel вызывает метод `aggregate(Exchange oldExchange, Exchange newExchange)` много раз — каждый раз, когда приходит очередная часть данных.

###### **Основная идея**
Каждый новый кусок результата поступает в `newExchange`, а текущий аккумулятор — в `oldExchange`.

Вы должны:
- вернуть новый `oldExchange` как агрегированный результат
- если `oldExchange == null`, значит это первое сообщение

---
Допустим, у вас есть массив:
```
[10, 20, 30]
```

Вы вызываете `.split(body())`

Camel будет вызывать AggregationStrategy так:
```
aggregate(null, 10) → результат 10
aggregate(10, 20) → результат 30
aggregate(30, 30) → результат 60
```

###### **Пример Простая сумма чисел**
```java
public class SumAggregationStrategy implements AggregationStrategy {
    @Override
    public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

        Integer newValue = newExchange.getIn().getBody(Integer.class);

        if (oldExchange == null) {
            newExchange.getIn().setBody(newValue);
            return newExchange;
        }

        Integer oldValue = oldExchange.getIn().getBody(Integer.class);
        oldExchange.getIn().setBody(oldValue + newValue);

        return oldExchange;
    }
}
```

Использование:
```java
from("direct:start")
    .split(body()).aggregationStrategy(new SumAggregationStrategy())
    .to("mock:result");
```


###### **Пример: Сбор JSON-объектов в список**
Многие так делают для REST-цепочек:
```java
public class CollectListStrategy implements AggregationStrategy {
    @Override
    public Exchange aggregate(Exchange oldExchange, Exchange newExchange) {

        List<Object> list;

        if (oldExchange == null) {
            list = new ArrayList<>();
            oldExchange = newExchange;
        } else {
            list = oldExchange.getIn().getBody(List.class);
        }

        list.add(newExchange.getIn().getBody());
        oldExchange.getIn().setBody(list);

        return oldExchange;
    }
}
```

Использование:
```java
from("direct:start")
    .split().body().aggregationStrategy(new CollectListStrategy())
    .log("Current = ${body}")
    .to("direct:invoke")
    .to("mock:done");
```
