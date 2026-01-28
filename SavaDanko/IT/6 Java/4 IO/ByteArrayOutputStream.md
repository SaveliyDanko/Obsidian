#java 

---
This class implements an output stream in which the data is written into a byte array. The buffer automatically grows as data is written to it.

###### 
```java
public ByteArrayOutputStream()
```
Creates a new `ByteArrayOutputStream`. The buffer capacity is initially 32 bytes, though its size increases if necessary.