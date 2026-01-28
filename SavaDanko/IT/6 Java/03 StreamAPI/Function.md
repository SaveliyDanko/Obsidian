---
tags:
  - review
sr-due: 2026-01-29
sr-interval: 1
sr-ease: 230
---

---
```java
@FunctionalInterface 
public interface Function<T,R>
```
Represents a function that accepts one argument and produces a result.

**apply**
```java
R apply(T t)
```
Applies this function to the given argument.

**compose**
```java
default <V> Function<V,R> compose(Function<? super V, ? extends T> before)
```
Returns a composed function that first applies the `before` function to its input, and then applies this function to the result.

**andThen**
```java
default <V> Function<T,V> andThen(Function<? super R, ? extends V> after)
```
Returns a composed function that first applies this function to its input, and then applies the after function to the result.

**identity**
```java
static <T> Function<T,T> identity()
```
Returns a function that always returns its input argument.

