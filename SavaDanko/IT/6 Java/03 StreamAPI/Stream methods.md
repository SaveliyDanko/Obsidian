#java 

---
###### **filter**
```java
Stream<T> filter(Predicate<? super T> predicate)
```
Returns a stream consisting of the elements of this stream that match the given predicate.

###### **map**
```java
<R> Stream<R> map(Function<? super T, ? extends R> mapper)
```
Returns a stream consisting of the results of applying the given function to the elements of this stream.

###### **flatMap**
```java
<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)
```
The `flatMap()` operation has the effect of applying a one-to-many transformation to the elements of the stream, and then flattening the resulting elements into a new stream.

```java
List<List<String>> list = List.of(
    List.of("Java", "Kotlin"),
    List.of("Python"),
    List.of("Go", "Rust")
);

List<String> flat = list.stream()
    .flatMap(Collection::stream)
    .toList();

System.out.println(flat);
// [Java, Kotlin, Python, Go, Rust]
```

###### **distinct**
Метод `distinct()` удаляет дубликаты из потока, оставляя только уникальные элементы, по определению метода `equals()`.
```java
Stream<T> distinct()
```

###### **sorted**
```java
Stream<T> sorted()
```
Returns a stream consisting of the elements of this stream, sorted according to natural order. If the elements of this stream are not `Comparable`, a `java.lang.ClassCastException` may be thrown when the terminal operation is executed.

```java
Stream<T> sorted(Comparator<? super T> comparator)
```

###### **peek**
```java
Stream<T> peek(Consumer<? super T> action)
```
Returns a stream consisting of the elements of this stream, additionally performing the provided action on each element as elements are consumed from the resulting stream.

###### **limit**
```java
Stream<T> limit(long maxSize)
```
Returns a stream consisting of the elements of this stream, truncated to be no longer than `maxSize` in length.

###### **skip**
```java
Stream<T> skip(long n)
```
Returns a stream consisting of the remaining elements of this stream after discarding the first `n` elements of the stream. If this stream contains fewer than `n` elements then an empty stream will be returned.

###### **forEach**
```java
void forEach(Consumer<? super T> action)
```
Performs an action for each element of this stream.

###### **toArray**
```java
Object[] toArray()
```
Returns an array containing the elements of this stream.

###### **reduce**
Метод `reduce()` выполняет агрегацию (свёртку) элементов потока до одного результата, объединяя элементы с помощью ассоциативной функции.

```java
Optional<T> reduce(BinaryOperator<T> accumulator)
```
Без начального значения. Возвращает `Optional<T>` (может быть пустым поток).
```java
Stream<Integer> stream = Stream.of(1, 2, 3, 4);
Optional<Integer> result = stream.reduce((a, b) -> a + b);
System.out.println(result.get()); // 10
```

```java
T reduce(T identity, BinaryOperator<T> accumulator)
```
С начальными значением (identity). Не возвращает Optional.
```java
int sum = Stream.of(1, 2, 3, 4)
    .reduce(0, (a, b) -> a + b);
System.out.println(sum); // 10
```

```java
<U> U reduce(U identity, BiFunction<U, ? super T, U> accumulator, BinaryOperator<U> combiner)
```
Форма для параллельных стримов (но работает и в обычных)

| Параметр      | Назначение                                                                 |
| ------------- | -------------------------------------------------------------------------- |
| `identity`    | начальное значение (единица для свёртки, не влияет на результат)           |
| `accumulator` | функция, накопливающая результат: `(состояние, элемент) → новое состояние` |
| `combiner`    | функция, объединяющая частичные результаты (особенно в `parallelStream`)   |
```java
List<String> words = List.of("Hello", "world", "from", "Stream");

String result = words.parallelStream()
    .reduce(
        "",                                   // identity
        (s1, s2) -> s1.isEmpty() ? s2 : s1 + " " + s2, // аккумулируем
        (s1, s2) -> s1 + " " + s2             // объединяем части
    );

System.out.println(result);
// "Hello world from Stream"
```

###### **collect**
Метод `collect()` — это терминальная операция в `Stream`, которая преобразует поток элементов в один итоговый результат (например, в `List`, `Set`, `Map`, строку и т. д.).
```java
<R, A> R collect(Collector<? super T, A, R> collector)
```

```java
Set<Integer> unique = Stream.of(1, 2, 2, 3)
    .collect(Collectors.toSet());

System.out.println(unique); // [1, 2, 3]
```

```java
Map<String, Integer> map = Stream.of("a", "bb", "ccc")
    .collect(Collectors.toMap(
        str -> str,          // ключ — строка
        String::length        // значение — длина строки
    ));

System.out.println(map); // {a=1, bb=2, ccc=3}
```

###### **toList**
```java
default List<T> toList()
```
Accumulates the elements of this stream into a `List`.

###### **min**
```java
Optional<T> min(Comparator<? super T> comparator)
```
Returns the minimum element of this stream according to the provided `Comparator`.

###### **max**
```java
Optional<T> max(Comparator<? super T> comparator)
```
Returns the maximum element of this stream according to the provided `Comparator`.

###### **count**
```java
long count()
```
Returns the count of elements in this stream.

###### **anyMatch**
```java
boolean anyMatch(Predicate<? super T> predicate)
```
Returns whether any elements of this stream match the provided predicate.

###### **allMatch**
```java
boolean allMatch(Predicate<? super T> predicate)
```
Returns whether all elements of this stream match the provided predicate.

###### **noneMatch**
```java
boolean noneMatch(Predicate<? super T> predicate)
```
Returns whether no elements of this stream match the provided predicate.

###### **findFirst**
```java
Optional<T> findFirst()
```
Returns an [`Optional`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Optional.html "class in java.util") describing the first element of this stream, or an empty `Optional` if the stream is empty.

###### **findAny**
```java
[Optional](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Optional.html "class in java.util")<[T](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/Stream.html#type-param-T "type parameter in Stream")> findAny()
```
Returns an [`Optional`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Optional.html "class in java.util") describing some element of the stream, or an empty `Optional` if the stream is empty.

###### **empty**
```java
static <T> Stream<T> empty()
```
Returns an empty sequential `Stream`.

###### **of**
```java
static <T> Stream<T> of(T... values)
```
Returns a sequential ordered stream whose elements are the specified values.

###### **generate**
```java
static <T> Stream<T> generate(Supplier<? extends T> s)
```
Returns an infinite sequential unordered stream where each element is generated by the provided `Supplier`.

###### **concat**
```java
static <T> Stream<T> concat(Stream<? extends T> a,
												Stream<? extends T> b)
```
Creates a lazily concatenated stream whose elements are all the elements of the first stream followed by all the elements of the second stream.