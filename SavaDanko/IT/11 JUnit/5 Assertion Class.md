---
tags:
  - review
sr-due: 2026-04-04
sr-interval: 76
sr-ease: 250
---

---
Класс `Assertions` в JUnit 5 предоставляет набор статических методов для проверки ожидаемых и фактических значений в тестах.

| Метод                                         | Назначение                                             |
| --------------------------------------------- | ------------------------------------------------------ |
| `assertEquals(expected, actual)`              | Проверяет равенство значений                           |
| `assertNotEquals(expected, actual)`           | Проверяет неравенство значений                         |
| `assertTrue(condition)`                       | Проверяет, что условие истинно                         |
| `assertFalse(condition)`                      | Проверяет, что условие ложно                           |
| `assertNull(object)`                          | Проверяет, что объект равен `null`                     |
| `assertNotNull(object)`                       | Проверяет, что объект не равен `null`                  |
| `assertThrows(expectedException, executable)` | Проверяет выброс исключения                            |
| `assertDoesNotThrow(executable)`              | Проверяет, что исключение не выбрасывается             |
| `assertArrayEquals(expected, actual)`         | Проверяет равенство массивов                           |
| `assertIterableEquals(expected, actual)`      | Проверяет равенство коллекций                          |
| `assertSame(expected, actual)`                | Проверяет, что оба объекта ссылаются на один экземпляр |
| `assertNotSame(expected, actual)`             | Проверяет, что объекты разные                          |
| `assertAll(executables...)`                   | Группирует несколько проверок                          |
| `fail(message)`                               | Принудительно проваливает тест                         |
