**Testing exceptions** — это процесс проверки того, что метод должен (или не должен) выбрасывать определённое исключение.

###### **`assertThrows`**
Это самый удобный и рекомендуемый способ тестировать исключения.
```java
assertThrows(IllegalArgumentException.class, () -> {
    service.process(null);
});
```
Что делает `assertThrows`:
- запускает указанный код (лямбду)
- проверяет, что было выброшено именно указанное исключение (или его подкласс)
- возвращает объект исключения, чтобы можно было проверить сообщение

###### **Проверка сообщения исключения**
`assertThrows` возвращает пойманное исключение:
```java
Exception ex = assertThrows(IllegalArgumentException.class, () -> {
    validator.validateAge(-5);
});

assertEquals("Age must be positive", ex.getMessage());
```