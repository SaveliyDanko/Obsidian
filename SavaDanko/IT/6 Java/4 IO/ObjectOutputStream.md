#java 

---
An ObjectOutputStream writes primitive data types and graphs of Java objects to an OutputStream.
Only objects that support the java.io.Serializable interface can be written to streams.
The method `writeObject` is used to write an object to the stream.
```java
try (FileOutputStream fos = new FileOutputStream("t.tmp");
		ObjectOutputStream oos = new ObjectOutputStream(fos)) {
        oos.writeObject("Today");
	    oos.writeObject(LocalDateTime.now());
} catch (Exception ex) {
		// handle exception
}
```

###### **ObjectOutputStream**
```java
public ObjectOutputStream(OutputStream out)
                   throws IOException
```
Creates an ObjectOutputStream that writes to the specified OutputStream.

###### **writeObject**
```java
public final void writeObject(Object obj)
                       throws IOException
```
Write the specified object to the ObjectOutputStream.

###### **flush**
```java
public void flush()
           throws IOException
```
Flushes the stream. This will write any buffered output bytes and flush through to the underlying stream.