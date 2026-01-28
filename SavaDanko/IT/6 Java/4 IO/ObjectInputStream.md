#java 

---
An ObjectInputStream deserializes primitive data and objects previously written using an ObjectOutputStream.
```java
try (FileInputStream fis = new FileInputStream("t.tmp");
		ObjectInputStream ois = new ObjectInputStream(fis)) {
        String label = (String) ois.readObject();
        LocalDateTime dateTime = (LocalDateTime) ois.readObject();
		// Use label and dateTime
} catch (Exception ex) {
		// handle exception
}
```

###### **ObjectInputStream**
```java
public ObjectInputStream(InputStream in)
                  throws IOException
```
Creates an ObjectInputStream that reads from the specified InputStream.

###### **readObject**
```java
public final Object readObject()
                        throws IOException,
									ClassNotFoundException
```
Read an object from the ObjectInputStream.

