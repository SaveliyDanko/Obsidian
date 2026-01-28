---
tags:
  - review
sr-due: 2026-03-07
sr-interval: 55
sr-ease: 250
---

---
AssertJ предоставляет удобные методы для проверки исключений в тестах на Java.

###### `assertThatThrownBy()`
- Проверяет, что блок кода выбрасывает исключение.
- Позволяет проверить тип исключения и сообщение.
```java
assertThatThrownBy(() -> {
    // код, который выбрасывает исключение
}).isInstanceOf(ExpectedException.class)
  .hasMessageContaining("expected message");
```

###### `assertThatExceptionOfType()`
- Упрощенная версия для проверки конкретного типа исключения.
```java
assertThatExceptionOfType(ExpectedException.class)
    .isThrownBy(() -> {
        // код, который выбрасывает исключение
    }).withMessage("expected message");
```

###### `assertThatCode().doesNotThrowAnyException()`
- Проверяет, что блок кода не выбрасывает никаких исключений.
```java
assertThatCode(() -> {
    // код, который не должен выбрасывать исключений
}).doesNotThrowAnyException();
```