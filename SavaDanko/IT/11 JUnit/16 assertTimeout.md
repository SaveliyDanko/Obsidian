---
tags:
  - review
sr-due: 2026-05-01
sr-interval: 94
sr-ease: 250
---

---
`assertTimeout` — это метод, который позволяет проверить, что код выполнится за ограниченное время. Если выполнение превышает заданный лимит, тест проваливается.
```java
assertTimeout(Duration.ofMillis(100), () -> {
    methodThatShouldBeFast();
});
```
Если `methodThatShouldBeFast()` выполняется дольше 100 мс — тест упадёт.

###### **Разница между `assertTimeout` и `assertTimeoutPreemptively`**
`assertTimeout(duration, executable)`
НЕ прерывает выполнение тестируемого кода.
Сначала код выполнится полностью, и только потом JUnit проверит, сколько времени он занял.

`assertTimeoutPreemptively(duration, executable)`
— прерывает выполнение, если время превышено.