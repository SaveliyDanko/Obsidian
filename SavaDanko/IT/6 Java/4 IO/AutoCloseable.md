---
tags:
  - review
---

---
An object that may hold resources (such as file or socket handles) until it is closed. The `close()` method of an `AutoCloseable` object is called automatically when exiting a `try`-with-resources block for which the object has been declared in the resource specification header.

```java
public interface AutoCloseable {  
		void close() throws Exception;  
}
```

###### **close**
Closes this resource, relinquishing any underlying resources. This method is invoked automatically on objects managed by the `try`-with-resources statement.