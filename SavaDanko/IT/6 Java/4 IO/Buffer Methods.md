#java 

---
###### **capacity**
```java
public final int capacity(){}
```
Returns this buffer's capacity.

###### **position**
```java
public final int position()
```
Returns this buffer's position.

###### **position**
```java
public Buffer position(int newPosition)
```
Sets this buffer's position. If the mark is defined and larger than the new position then it is discarded.

###### **limit**
```java
public final int limit()
```
Returns this buffer's limit.

###### **limit**
```java
public Buffer limit(int newLimit)
```
Sets this buffer's limit.
The new limit value must be non-negative and no larger than this buffer's capacity

###### **mark**
```java
public Buffer mark()
```
Sets this buffer's mark at its position.

###### **reset**
```java
public Buffer reset()
```
Resets this buffer's position to the previously-marked position.

###### **clear**
```java
public Buffer clear()
```
Clears this buffer. The position is set to zero, the limit is set to the capacity, and the mark is discarded.

###### **flip**
```java
public Buffer flip()
```
Flips this buffer. The limit is set to the current position and then the position is set to zero. If the mark is defined then it is discarded.
###### **rewind**
```java
public Buffer rewind()
```
Rewinds this buffer. The position is set to zero and the mark is discarded.

###### **remaining**
```java
public final int remaining()
```
Returns the number of elements between the current position and the limit.

###### **hasRemaining**
```java
public final boolean hasRemaining()
```
Tells whether there are any elements between the current position and the limit.

###### **isReadOnly**
```java
public abstract boolean isReadOnly()
```
Tells whether or not this buffer is read-only.

###### **hasArray**
```java
public abstract boolean hasArray()
```
Tells whether or not this buffer is backed by an accessible array.


###### **array**
```java
public abstract Object array()
```
Returns the array that backs this buffer.
This method is intended to allow array-backed buffers to be passed to native code more efficiently.

###### **isDirect**
```java
public abstract boolean isDirect()
```
Tells whether or not this buffer is `direct`.

###### **slice**
```java
public abstract Buffer slice()
```
Creates a new buffer whose content is a shared subsequence of this buffer's content.
The content of the new buffer will start at position `index` in this buffer, and will contain `length` elements. Changes to this buffer's content will be visible in the new buffer, and vice versa; the two buffers' position, limit, and mark values will be independent.

###### **slice**
```java
public abstract Buffer slice(int index,
											int length)
```
Creates a new buffer whose content is a shared subsequence of this buffer's content.

###### **dublicate**
```java
public abstract Buffer duplicate()
```
Creates a new buffer that shares this buffer's content.
The content of the new buffer will be that of this buffer. Changes to this buffer's content will be visible in the new buffer, and vice versa; the two buffers' position, limit, and mark values will be independent.