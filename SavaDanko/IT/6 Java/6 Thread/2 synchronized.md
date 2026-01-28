---
tags:
  - review
---

---
В Java ключевое слово `synchronized` используется для синхронизации доступа к критическим участкам кода, чтобы предотвратить одновременное выполнение этого кода несколькими потоками. Это необходимо для защиты общего ресурса от состояния гонки (race condition).
1. Только один поток может выполнять `synchronized`-блок или метод в один момент времени.
2. Потоки получают видимость актуальных значений переменных.
    

#### Виды `synchronized` методов
**Synchronized instance method**
```java
public synchronized void increment() {
    counter++;
}
```

**Synchronized static method**
```java
public static synchronized void log(String msg) {
    System.out.println(msg);
}
```
Блокировка происходит на объекте класса `ClassName.class`, т.е. на метаклассе.
Полезно, если несколько потоков работают с одним статическим ресурсом.

**Synchronized block (блок внутри метода)**
```java
public void write(String value) {
    synchronized (this) {
        this.data = value;
    }
}
```
Можно ограничить область синхронизации только тем участком, где она действительно нужна.

**Синхронизация на произвольных объектах**
```java
private final Object lock = new Object();

public void write(String value) {
    synchronized (lock) {
        this.data = value;
    }
}
```
