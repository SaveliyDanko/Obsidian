---
tags:
  - review
sr-due: 2026-03-22
sr-interval: 65
sr-ease: 250
---

---
Аннотация `@Tag` в JUnit 5 используется для маркировки тестов с целью их группировки и последующего избирательного выполнения. Она позволяет запускать только определенные тесты по заданным меткам (тегам).

###### **Настройка запуска тестов по тегам:**
```groovy
test {
    useJUnitPlatform {
        includeTags 'fast', 'unit'
        excludeTags 'slow', 'integration'
    }
}
```

###### **Использование аннотации @Tag:**
```java
public class TagExampleTest {
    @Test
    @Tag("fast")
    @Tag("unit")
    void fastTest() {
        System.out.println("Fast test executed");
    }

    @Test
    @Tag("slow")
    void slowTest() {
        System.out.println("Slow test executed");
    }
}
```