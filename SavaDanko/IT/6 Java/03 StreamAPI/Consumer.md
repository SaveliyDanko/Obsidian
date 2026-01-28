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
public interface Consumer<T>
```
Represents an operation that accepts a single input argument and returns no result.

**accept**
```java
void accept(T t)
```
Performs this operation on the given argument.

**andThen**
```java
default Consumer<T> andThen(Consumer<? super T> after)
```
Returns a composed `Consumer` that performs, in sequence, this operation followed by the `after` operation.