---
tags:
  - review
sr-due: 2026-03-25
sr-interval: 69
sr-ease: 250
---

---
`Cache<K, V>` — это основной интерфейс синхронного кэша в библиотеке Caffeine.

Это обёртка над высокопроизводительной ConcurrentHashMap с встроенной политикой вытеснения, статистикой, ограничениями и возможностью авто-загрузки значений.

###### **get / getIfPresent**
```java
V getIfPresent(K key)
V get(K key, Function<? super K, ? extends V> mappingFunction)
```

###### **put / invalidate**
```java
void put(K key, V value)
void invalidate(K key)
void invalidateAll()
```

###### **policy — доступ к LRU/LFU-алгоритмам**
Через `cache.policy()` можно посмотреть:
- размер
- какие ключи в буфере записи
- что недавно вытеснилось

###### **stats()**
Если включена статистика:
```java
CacheStats stats = cache.stats();
```
Показывает hit rate, miss rate, eviction count