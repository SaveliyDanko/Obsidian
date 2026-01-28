---
tags:
  - review
sr-due: 2026-03-31
sr-interval: 64
sr-ease: 250
---

---
`@Autowired` — это аннотация Spring, которая говорит контейнеру:
> Найди подходящий бин и внедри его в это место.
> Spring просканирует свои бины, найдёт подходящий по типу объект и передаст его автоматически.

```java
@Component
public class Engine {
    public String getType() {
        return "V8";
    }
}

@Component
public class Car {
    private final Engine engine;

    @Autowired
    public Car(Engine engine) {
        this.engine = engine;
    }

    public void drive() {
        System.out.println("Driving with engine: " + engine.getType());
    }
}
```
- `Car` зависит от `Engine`.
- Spring создаст `Engine` и передаст его в `Car` — автоматически

###### **Где можно использовать `@Autowired`**

| Где?           | Пример                                                  |
| -------------- | ------------------------------------------------------- |
| В конструкторе | `@Autowired public MyBean(Dependency dep) { ... }`      |
| В сеттере      | `@Autowired public void setDep(Dependency dep) { ... }` |
| В поле         | `@Autowired private Dependency dep;`                    |

> Лучше использовать через конструктор — это современный и безопасный способ.

###### **Как Spring находит, что внедрять?**
- Spring ищет бин подходящего типа.
- Если один такой бин — всё работает.
- Если несколько — Spring не знает, что выбрать → ошибка.