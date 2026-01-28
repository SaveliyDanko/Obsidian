#java 

---
**`Map<K, V>`** — это структура данных, которая хранит пары ключ → значение.

###### Интерфейс `Map<K, V>`
- `K` — тип ключей
- `V` — тип значений

###### Реализации:
[[HashMap]]
`LinkedHashMap` - Сохраняет порядок вставки
`TreeMap` - Отсортирован по ключам
`ConcurrentHashMap` - Потокобезопасная `HashMap`

###### Методы
```java
void clear();

boolean containsKey(Object key);

boolean containsValue(Object value);

Set<Map.Entry<K, V>> entrySet();

V get(Object key);

int size();

boolean isEmpty();

V put(K key, V value);

V remove(Object key);

void clear();

Set<K> keySet();

Collection<V> values();
```