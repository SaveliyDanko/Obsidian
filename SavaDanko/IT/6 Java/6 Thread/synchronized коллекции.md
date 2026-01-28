synchronized коллекции - это коллекции из пакета `java.util`, к которым добавлены мониторные блокировки (`synchronized`) для защиты операций от состояния гонки.

Java предоставляет обертки через `Collections.synchronizedXXX(...)`:
```java
List<String> syncList = Collections.synchronizedList(new ArrayList<>());
Map<String, Integer> syncMap = Collections.synchronizedMap(new HashMap<>());
Set<String> syncSet = Collections.synchronizedSet(new HashSet<>());
```
Все методы (например, `add()`, `get()`, `put()`) этих коллекций синхронизированы изнутри.

**итерация НЕ потокобезопасна**
Даже если сама коллекция синхронизирована, итерация по ней должна происходить в `synchronized` блоке вручную:
```java
synchronized (syncList) {
    for (String item : syncList) {
        System.out.println(item);
    }
}
```

