---
tags:
  - review
---

---
**Reentrance** означает: поток, который уже захватил монитор, может войти в него ещё раз — без блокировки

То есть один и тот же поток может:
- повторно войти в `synchronized`-блок
- вызвать `synchronized`-метод
- вызвать другой `synchronized`-метод того же объекта
```java
class Counter {
    synchronized void inc() {
        log();     // ← тоже synchronized
        value++;
    }

    synchronized void log() {
        System.out.println(value);
    }

    private int value = 0;
}
```
- Поток заходит в `inc()` → захватывает монитор `this`
- Внутри вызывает `log()`
- `log()` тоже `synchronized`
- Но блокировки нет, потому что монитор уже принадлежит этому же потоку