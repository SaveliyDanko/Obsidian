#java 

---
A `Flushable` is a destination of data that can be flushed. The flush method is invoked to write any buffered output to the underlying stream.
```java
public interface Flushable {  
}
```

###### **flush**
```java
void flush() throws IOException;  
```
Flushes this stream by writing any buffered output to the underlying stream.