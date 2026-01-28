
#java 

---
We use `PrintStream` when we need a convenient way to write characters and strings to an `OutputStream`, especially when working with byte-oriented output. However, `PrintStream` does not support specifying character encodings directly, as it writes raw bytes. In contrast, `PrintWriter` is designed for character-based output and allows encoding control when used with an `OutputStreamWriter`.
```java
public class PrintStream
					extends FilterOutputStream
					implements Appendable, Closeable
```

###### **PrintStream**
```java
public PrintStream(OutputStream out)
```

###### **print**
```java
public void print(String s)
```
Prints a string.

###### **print**
```java
public void print(Object obj)
```
Prints an object.

###### **println**
```java
public void println(String x)
```