---
tags:
  - review
sr-due: 2026-04-13
sr-interval: 80
sr-ease: 250
---

---
**Listeners** в Caffeine — это обработчики событий кэша

Они позволяют реагировать на события, которые происходят внутри кэша — например, когда запись удаляется, вытесняется или обновляется.

###### **Основные типы слушателей:**
- RemovalListener — вызывается, когда запись удаляется (по eviction, expiration, invalidate).
- EvictionListener — вызывается при вытеснении по размеру/весу.

###### **Пример:**
```java
Caffeine.newBuilder()
    .removalListener((key, value, cause) ->
        System.out.println("Removed: " + key + ", cause: " + cause))
    .build();
```