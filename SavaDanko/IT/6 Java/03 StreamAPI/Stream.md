#java 

---
[Stream Doc](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/Stream.html#method-summary)
[java.util.stream Doc](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/package-summary.html#Parallelism)

---
**Stream** $-$ A sequence of elements supporting sequential and parallel aggregate operations.

In addition to `Stream`, which is a stream of object references, there are primitive specializations for [`IntStream`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/IntStream.html "interface in java.util.stream"), [`LongStream`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/LongStream.html "interface in java.util.stream"), and [`DoubleStream`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/DoubleStream.html "interface in java.util.stream"), all of which are referred to as "streams" and conform to the characteristics and restrictions described here.

To perform a computation, stream [operations](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/package-summary.html#StreamOps) are composed into a _stream pipeline_. A stream pipeline consists of a source (which might be an array, a collection, a generator function, an I/O channel, etc), zero or more _intermediate operations_ (which transform a stream into another stream, such as [`filter(Predicate)`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/Stream.html#filter\(java.util.function.Predicate\))), and a _terminal operation_ (which produces a result or side-effect, such as [`count()`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/Stream.html#count\(\)) or [`forEach(Consumer)`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/Stream.html#forEach\(java.util.function.Consumer\))). Streams are lazy; computation on the source data is only performed when the terminal operation is initiated, and source elements are consumed only as needed.

Реализация стримов имеет широкую свободу в оптимизации вычислений результата.  
Например, реализация может исключить (*elide*) некоторые операции или целые этапы стрим-конвейера, если может доказать, что это не повлияет на конечный результат.
Это означает, что побочные эффекты (*side-effects*) в лямбда-выражениях могут быть не выполнены — и на них нельзя полагаться, если только не указано явно, как это сделано, например, для терминальных операций `forEach` и `forEachOrdered`.

Хотя коллекции и стримы внешне похожи, они преследуют разные цели.
- Коллекции предназначены прежде всего для эффективного управления элементами и доступа к ним (например, получить по индексу, добавить, удалить и т.д.).
- В отличие от них, стримы не позволяют напрямую получать или изменять элементы.  
    Их задача — декларативно описывать источник данных и указать, какие операции обработки нужно выполнить над этими данными в совокупности.

Stream pipelines may execute either sequentially or in [parallel](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/package-summary.html#Parallelism). This execution mode is a property of the stream. Streams are created with an initial choice of sequential or parallel execution. (For example, [`Collection.stream()`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Collection.html#stream\(\)) creates a sequential stream, and [`Collection.parallelStream()`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/Collection.html#parallelStream\(\)) creates a parallel one.) This choice of execution mode may be modified by the [`BaseStream.sequential()`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/BaseStream.html#sequential\(\)) or [`BaseStream.parallel()`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/BaseStream.html#parallel\(\)) methods, and may be queried with the [`BaseStream.isParallel()`](https://docs.oracle.com/en/java/javase/24/docs/api/java.base/java/util/stream/BaseStream.html#isParallel\(\)) method.