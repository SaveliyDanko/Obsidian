#java 

---
This class defines six categories of operations upon byte buffers:
- Absolute and relative `get` and `put` methods that read and write single bytes
- Absolute and relative `bulk get` methods that transfer contiguous sequences of bytes from this buffer into an array
- Absolute and relative `bulk put` methods that transfer contiguous sequences of bytes from a byte array or some other byte buffer into this buffer
- Absolute and relative `get` and `put` methods that read and write values of other primitive types, translating them to and from sequences of bytes in a particular byte order
- Methods for creating view buffers, which allow a byte buffer to be viewed as a buffer containing values of some other primitive type
- A method for compacting a byte buffer
Byte buffers can be created either by `allocation`, which allocates space for the buffer's content, or by `wrapping` an existing byte array into a buffer.

###### **Direct vs Non-direct buffers**
A byte buffer is either direct or non-direct. Given a direct byte buffer, the Java virtual machine will make a best effort to perform native I/O operations directly upon it. That is, it will attempt to avoid copying the buffer's content to (or from) an intermediate buffer before (or after) each invocation of one of the underlying operating system's native I/O operations.
A direct byte buffer may be created by invoking the `allocateDirect` factory method of this class. The buffers returned by this method typically have somewhat higher allocation and deallocation costs than non-direct buffers.
The contents of direct buffers may reside outside of the normal garbage-collected heap, and so their impact upon the memory footprint of an application might not be obvious.
It is therefore recommended that direct buffers be allocated primarily for large, long-lived buffers that are subject to the underlying system's native I/O operations.
In general it is best to allocate direct buffers only when they yield a measurable gain in program performance.

A direct byte buffer may also be created by mapping a region of a file directly into memory.
An implementation of the Java platform may optionally support the creation of direct byte buffers from native code via JNI.
Whether a byte buffer is direct or non-direct may be determined by invoking its `isDirect()` method. This method is provided so that explicit buffer management can be done in performance-critical code.

###### **Access to binary data**
This class defines methods for reading and writing values of all other primitive types, except `boolean`. Primitive values are translated to (or from) sequences of bytes according to the buffer's current byte order, which may be retrieved and modified via the `order` methods. Specific byte orders are represented by instances of the `ByteOrder` class. The initial order of a byte buffer is always `BIG_ENDIAN`.

For access to heterogeneous binary data, that is, sequences of values of different types, this class defines a family of absolute and relative `get` and `put` methods for each type.

---
###### **allocateDirect**
```java
public static ByteBuffer allocateDirect(int capacity){}
```
Allocates a new direct byte buffer.

###### **allocate**
```java
public static ByteBuffer allocate(int capacity)
```
Allocates a new byte buffer.

###### **wrap**
```java
public static ByteBuffer wrap(byte[] array,
												 int offset,
												 int length)
```
Wraps a byte array into a buffer.

###### **asReadOnlyBuffer**
```java
public abstract ByteBuffer asReadOnlyBuffer()
```
Creates a new, read-only byte buffer that shares this buffer's content.

###### **get**
```java
public abstract byte get()
```

###### **put**
```java
public abstract ByteBuffer put(byte b)
```

###### **compact**
```java
public abstract ByteBuffer compact()
```


