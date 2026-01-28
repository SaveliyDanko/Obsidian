#java 

---
A `ByteArrayInputStream` contains an internal buffer that contains bytes that may be read from the stream.
```java
public class ByteArrayInputStream
					extends InputStream
```
###### **ByteArrayInputStream**
```java
public ByteArrayInputStream(byte[] buf)
```
Creates a `ByteArrayInputStream` so that it uses `buf` as its buffer array.

```java
public ByteArrayInputStream(byte[] buf,
												 int offset,
												 int length)
```