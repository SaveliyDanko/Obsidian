---
tags:
  - review
sr-due: 2026-01-26
sr-interval: 15
sr-ease: 230
---

---
Аннотация `@TestMethodOrder` используется для задания порядка выполнения тестовых методов в классе. По умолчанию порядок выполнения тестов в JUnit **неопределённый**, но с помощью этой аннотации можно явно указать нужный порядок.

---
###### **Когда использовать @TestMethodOrder:**
- Когда порядок выполнения тестов имеет значение (например, в интеграционных тестах).
- При проверке работы системы в пошаговом режиме.
- Когда тесты зависят друг от друга (не рекомендуется, но иногда необходимо).
- Для создания демонстрационных или учебных примеров.

###### **Синтаксис и использование @TestMethodOrder:**
```java
import org.junit.jupiter.api.*;

@TestMethodOrder(MethodOrderer.OrderAnnotation.class)
public class OrderedTest {

    @Test
    @Order(2)
    void secondTest() {
        System.out.println("Второй тест");
    }

    @Test
    @Order(1)
    void firstTest() {
        System.out.println("Первый тест");
    }

    @Test
    @Order(3)
    void thirdTest() {
        System.out.println("Третий тест");
    }
}
```

###### **Результат выполнения:**
```
Первый тест
Второй тест
Третий тест
```
