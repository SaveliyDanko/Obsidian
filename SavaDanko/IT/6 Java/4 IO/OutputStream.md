#java 

---
This abstract class is the superclass of all classes representing an output stream of bytes. An output stream accepts output bytes and sends them to some sink.
```java
public abstract class OutputStream implements Closeable, Flushable {
}
```

###### **write**
```java
public void write(byte[] b, int off, int len) throws IOException {  
}
```
Writes `len` bytes from the specified byte array starting at offset `off` to this output stream.

###### **flush**
```java
public void flush() throws IOException {  
}
```
Flushes this output stream and forces any buffered output bytes to be written out

###### **close**
```java
public void close() throws IOException {  
}
```
Closes this output stream and releases any system resources associated with this stream.