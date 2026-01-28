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
public interface Predicate<T>
```
Represents a predicate (boolean-valued function) of one argument.

**test**
```java
boolean test(T t)
```
Evaluates this predicate on the given argument.

**and**
```java
default Predicate<T> and(Predicate<? super T> other)
```

**or**
```java
default Predicate<T> or(Predicate<? super T> other)
```

**negate**
```java
default Predicate<T> negate()
```
Returns a predicate that represents the logical negation of this predicate.

**isEqual**
```java
static <T> Predicate<T> isEqual(Object targetRef)
```
Returns a predicate that tests if two arguments are equal according to Objects.equals(Object, Object).

```java
Predicate<String> isHello = Predicate.isEqual("hello");

System.out.println(isHello.test("hello")); // true
System.out.println(isHello.test("HELLO")); // false

```

**not**
```java
static <T> Predicate<T> not(Predicate<? super T> target)
```
Returns a predicate that is the negation of the supplied predicate. This is accomplished by returning result of the calling `target.negate()`.
