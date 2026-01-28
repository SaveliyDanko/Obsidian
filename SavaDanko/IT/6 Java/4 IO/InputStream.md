#java 

---
This abstract class is the superclass of all classes representing an input stream of bytes.

Applications that need to define a subclass of `InputStream` must always provide a method that returns the next byte of input.

###### **read**
```java
public abstract int read() throws IOException;
```
Reads the next byte of data from the input stream. The value byte is returned as an `int` in the range `0` to `255`. If no byte is available because the end of the stream has been reached, the value `-1` is returned. This method blocks until input data is available, the end of the stream is detected, or an exception is thrown.

###### **read**
```java
public int read(byte[] b, int off, int len) throws IOException {  
}
```
Reads up to `len` bytes of data from the input stream into an array of bytes. An attempt is made to read as many as `len` bytes, but a smaller number may be read. The number of bytes actually read is returned as an integer.

###### **readAllBytes**
```java
public byte[] readAllBytes() throws IOException {  
}
```
Reads all remaining bytes from the input stream.

###### **skip**
```java
public long skip(long n) throws IOException {   
}
```
Skips over and discards `n` bytes of data from this input stream.

###### **available**
```java
public int available() throws IOException {
}
```
Returns an estimate of the number of bytes that can be read (or skipped over) from this input stream without blocking.

###### **mark**
```java
public void mark(int readlimit) {}
```
Marks the current position in this input stream. A subsequent call to the `reset` method repositions this stream at the last marked position so that subsequent reads re-read the same bytes.
The `readlimit` arguments tells this input stream to allow that many bytes to be read before the mark position gets invalidated.

###### **reset**
```java
public void reset() throws IOException {}
```
Repositions this stream to the position at the time the `mark` method was last called on this input stream.

###### **transferTo**
```java
public long transferTo(OutputStream out) throws IOException {}
```
Reads all bytes from this input stream and writes the bytes to the given output stream in the order that they are read.