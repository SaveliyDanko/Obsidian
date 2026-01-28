---
tags:
  - review
sr-due: 2026-01-28
sr-interval: 3
sr-ease: 250
---

---
[Optional Documentation](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Optional.html)

---
**Optional** — это объект-контейнер, который используется для представления того факта, что значение может отсутствовать (быть `null`). Он заставляет программиста явно обрабатывать ситуацию отсутствия данных, предотвращая знаменитую ошибку `NullPointerException`.

---
**empty**
```java
public static <T> Optional<T> empty()
```
Возвращает пустой экземпляр `Optional`. Внутри него нет значения.

**of**
```java
public static <T> Optional<T> of(T value)
```
Возвращает `Optional`, содержащий указанное значение.

**ofNullable**
```java
public static <T> Optional<T> ofNullable(T value)
```
Самый безопасный способ создания. Если переданное значение не равно `null`, возвращает `Optional` с этим значением. Если передать `null`, вернет пустой `Optional` (аналог `empty()`)

---
**isPresent**
```java
public boolean isPresent()
```
Возвращает `true`, если значение присутствует, иначе — `false`.

**isEmpty**
```java
public boolean isEmpty()
```
Обратный метод для `isPresent()`. Возвращает `true`, если значение отсутствует (контейнер пуст).

---
**get**
```java
public T get()
```
Если значение есть, возвращает его. Если значения нет, выбрасывает исключение `NoSuchElementException`.

**orElse**
```java
public T orElse(T other)
```
Возвращает значение, если оно есть. Если контейнер пуст, возвращает переданное значение `other` (значение по умолчанию).

**or**
```java
public Optional<T> or(Supplier<? extends Optional<? extends T>> supplier)
```
Похож на `orElse`, но возвращает не само значение `T`, а другой Optional.

**orElseThrow**
```java
public T orElseThrow(Supplier<? extends T> supplier)
```
Возвращает значение, если оно есть. Если пусто — выбрасывает исключение, которое создается переданным поставщиком.

**orElseGet**
```java
public T orElseGet(Supplier<? extends T> supplier)
```
Возвращает значение, если оно есть. Если пусто — вызывает функцию-поставщик (`supplier`) и возвращает её результат.