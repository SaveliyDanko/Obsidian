#java 

---
[java.util.stream Doc](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/package-summary.html)
[[Determinism]]

---
Classes to support functional-style operations on streams of elements.
- No storage. A stream is not a data structure that stores elements.
- Functional in nature. An operation on a stream produces a result, but does not modify its source.
- Laziness-seeking.
- Possibly unbounded.
- Consumable. The elements of a stream are only visited once during the life of a stream.

#### Stream operations and pipelines
Stream operations are divided into _intermediate_ and _terminal_ operations, and are combined to form _stream pipelines_.

A stream pipeline consists of a source followed by zero or more intermediate operations and a terminal operation.

Intermediate operations return a new stream. They are always _lazy_;

Terminal operations may traverse the stream to produce a result or a side-effect. Terminal operations are _eager_.

Intermediate operations are further divided into _stateless_ and _stateful_ operations. Stateless operations, such as `filter` and `map`, retain no state from previously seen element when processing a new element -- each element can be processed independently of operations on other elements. Stateful operations, such as `distinct` and `sorted`, may incorporate state from previously seen elements when processing new elements.

Further, some operations are deemed _short-circuiting_ operations. An intermediate operation is short-circuiting if, when presented with infinite input, it may produce a finite stream as a result. A terminal operation is short-circuiting if, when presented with infinite input, it may terminate in finite time.

#### Parallelism
Processing elements with an explicit `for-loop` is inherently serial.
Streams facilitate parallel execution by reframing the computation as a pipeline of aggregate operations, rather than as imperative operations on each individual element. All streams operations can execute either in serial or in parallel. The stream implementations in the JDK create serial streams unless parallelism is explicitly requested.
Collection has methods `Collection.stream()` and `Collection.parallelStream()`.

The stream pipeline is executed sequentially or in parallel depending on the mode of the stream on which the terminal operation is invoked.
The sequential or parallel mode of a stream can be determined with the `BaseStream.isParallel()` method, and the stream's mode can be modified with the `BaseStream.sequential()` and `BaseStream.parallel()` operations. The most recent sequential or parallel mode setting applies to the execution of the entire stream pipeline.

#### Non-interference
Streams enable you to execute possibly-parallel aggregate operations over a variety of data sources, including even non-thread-safe collections such as `ArrayList`. This is possible only if we can prevent _interference_ with the data source during the execution of a stream pipeline.

For most data sources, preventing interference means ensuring that the data source is _not modified at all_ during the execution of the stream pipeline. The notable exception to this are streams whose sources are concurrent collections, which are specifically designed to handle concurrent modification.

#### Side-effects
Many computations that might seem to require *side-effects* can often be rewritten without them, using tools like *reductions* instead of mutable variables.

```java
List<String> result = new ArrayList<>();
Stream.of("a", "b", "c").forEach(result::add); // side-effect
```

```java
List<String> result = Stream.of("a", "b", "c").collect(Collectors.toList());
```


#### Ordering
Streams may or may not have a defined _encounter order_.
Many operations will be processed faster in parallel mode if the stream flow is not important. Often parallel operations work efficiently even on ordered data.

#### Reduction operations
A _reduction_ operation (also called a _fold_) takes a sequence of input elements and combines them into a single summary result by repeated application of a combining operation, such as finding the sum or maximum of a set of numbers, or accumulating elements into a list. The streams classes have multiple forms of general reduction operations, called `reduce()` and `collect()`, as well as multiple specialized reduction forms such as `sum()`, `max()`, or `count()`.

```java
 <U> U reduce(U identity,
              BiFunction<U, ? super T, U> accumulator,
              BinaryOperator<U> combiner);
```
Here, the _identity_ element is both an initial seed value for the reduction and a default result if there are no input elements. The _accumulator_ function takes a partial result and the next element, and produces a new partial result. The _combiner_ function combines two partial results to produce a new partial result.

The mutable reduction operation is called `collect()`, as it collects together the desired results into a result container such as a `Collection`. A `collect` operation requires three functions: a supplier function to construct new instances of the result container, an accumulator function to incorporate an input element into a result container, and a combining function to merge the contents of one result container into another.
```java
 <R> R collect(Supplier<R> supplier,
               BiConsumer<R, ? super T> accumulator,
               BiConsumer<R, R> combiner);
```

We can use the abstraction of a `Collector` "interface in java.util.stream") to capture all three aspects.
```java
List<String> strings = stream.map(Object::toString)
                                  .collect(Collectors.toList());
```

#### Associativity
Associativity is very important for parallel computing.
`a op b op c op d = (a op b) op (c op d) = a op (b op c) op d`
We can arrive at a deterministic operation in an arbitrary order of application between objects.

#### Low-level stream construction
The class `StreamSupport` has a number of low-level methods for creating a stream, all using some form of a `Spliterator`. A spliterator is the parallel analogue of an `Iterator`; it describes a (possibly infinite) collection of elements, with support for sequentially advancing, bulk traversal, and splitting off some portion of the input into another spliterator which can be processed in parallel. At the lowest level, all streams are driven by a spliterator.