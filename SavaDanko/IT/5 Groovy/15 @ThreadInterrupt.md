---
tags:
  - review
sr-due: 2026-04-15
sr-interval: 81
sr-ease: 250
---

---
Аннотация `@ThreadInterrupt` автоматически вставляет проверки `Thread.currentThread().isInterrupted()` в стратегически важные места метода, чтобы код мог корректно реагировать на запросы прерывания потока.

Когда вы помечаете метод или класс этой аннотацией, Groovy AST-трансформация добавляет проверки прерывания в:
1. Начало циклов (for, while)
2. После определенного количества итераций в циклах
3. В начале блока finally

###### **Пример использования**
```groovy
import groovy.transform.ThreadInterrupt

@ThreadInterrupt
def longRunningTask() {
    for (int i = 0; i < 1000000; i++) {
        // Трудоемкие вычисления
        Math.sqrt(i)
    }
}
```

После трансформации код будет выглядеть примерно так:
```groovy
def longRunningTask() {
    for (int i = 0; i < 1000000; i++) {
        // Автоматически добавленная проверка
        if (Thread.currentThread().isInterrupted()) {
            throw new InterruptedException("Execution interrupted")
        }
        Math.sqrt(i)
    }
}
```