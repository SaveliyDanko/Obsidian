---
tags:
  - review
sr-due: 2026-04-07
sr-interval: 78
sr-ease: 250
---

---
[assertAll documentation](https://docs.junit.org/current/api/org.junit.jupiter.api/org/junit/jupiter/api/Assertions.html#assertAll(java.lang.String,java.util.stream.Stream))

---
`assertAll` — инструмент, который позволяет выполнять несколько проверок в одном тесте и при этом видеть все ошибки сразу, а не только первую.

Обычно, если в тесте идёт несколько asserts, выполнение остановится на первой же ошибке:
```java
assertEquals("Alice", user.getName());  // если упадёт — дальше код не пойдёт
assertEquals(25, user.getAge());
assertNotNull(user.getEmail());
```
Если первый assert упал — два других НЕ выполняются.

###### **`assertAll` решает эту проблему**
`assertAll` позволяет сгруппировать несколько проверок:
```java
assertAll(
    () -> assertEquals("Alice", user.getName()),
    () -> assertEquals(25, user.getAge()),
    () -> assertNotNull(user.getEmail())
);
```
Здесь:
- выполнимся все три lambda-функции
- JUnit соберёт все ошибки
- тест упадёт только после выполнения всех проверок
- отчёт покажет полный список провалов

###### **Сигнатура метода**
```java
assertAll(String heading, Executable... executables)
```
Можно указать заголовок (необязательно):
```java
assertAll("User validation",
    () -> assertEquals("Alice", user.getName()),
    () -> assertTrue(user.getAge() > 18)
);
```
