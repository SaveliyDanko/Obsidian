#java 

A `BufferedInputStream` adds functionality to another input stream-namely, the ability to buffer the input and to support the `mark` and `reset` methods.
```java
public class BufferedInputStream extends FilterInputStream{};
```

###### **BufferedInputStream**
```java
public BufferedInputStream(InputStream in)
```
Creates a `BufferedInputStream` and saves its argument, the input stream `in`, for later use. An internal buffer array is created and stored in `buf`.

###### **BufferedInputStream**
```java
public BufferedInputStream(InputStream in, int size)
```
Creates a `BufferedInputStream` with the specified buffer size.

###### **Example:**
```java
BufferedInputStream inputStream = 
							new BufferedInputStream(new FileInputStream("file.txt"))
```
