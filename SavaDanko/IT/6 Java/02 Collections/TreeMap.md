#java 

---
[[Map]]

---
**`TreeMap<K, V>`** — это отсортированная реализация интерфейса `Map`, где:
- пары "ключ → значение" хранятся в отсортированном порядке по ключам,
- сортировка основана на естественном порядке (`Comparable`) или переданном компараторе (`Comparator`).
- Основа Красно-Чёрное Дерево

| Метод                        | Назначение                              |
| ---------------------------- | --------------------------------------- |
| `firstKey()`                 | Вернуть самый маленький ключ            |
| `lastKey()`                  | Вернуть самый большой ключ              |
| `ceilingKey(K key)`          | Найти минимальный ключ ≥ переданному    |
| `floorKey(K key)`            | Найти максимальный ключ ≤ переданному   |
| `lowerKey(K key)`            | Найти максимальный ключ < переданному   |
| `higherKey(K key)`           | Найти минимальный ключ > переданному    |
| `subMap(K fromKey, K toKey)` | Подмножество от одного ключа до другого |
| `headMap(K toKey)`           | Все ключи меньше указанного             |
| `tailMap(K fromKey)`         | Все ключи больше или равны указанному   |


###### `TreeMap` с `Comparator`
```java
TreeMap<String, Integer> reverseMap = new TreeMap<>(Comparator.reverseOrder());

reverseMap.put("Banana", 3);
reverseMap.put("Apple", 5);
reverseMap.put("Cherry", 2);

System.out.println(reverseMap);  // {Cherry=2, Banana=3, Apple=5}
```
