#java 

---
A simple text scanner which can parse primitive types and strings using regular expressions.
A `Scanner` breaks its input into tokens using a delimiter pattern, which by default matches whitespace. The resulting tokens may then be converted into values of different types using the various `next` methods.
```java
public final class Scanner
							extends Object
							implements Iterator<String>, Closeable
```


###### **Scanner**
```java
public Scanner(Readable source)
```
Constructs a new `Scanner` that produces values scanned from the specified source.

###### **Scanner**
```java
public Scanner(InputStream source)
```
Constructs a new `Scanner` that produces values scanned from the specified input stream.

###### **Scanner**
```java
public Scanner(File source)
        throws FileNotFoundException
```
Constructs a new `Scanner` that produces values scanned from the specified file.

###### **hasNext**
```java
public boolean hasNext()
```
Returns true if this scanner has another token in its input.

###### **next**
```java
public String next()
```
Finds and returns the next complete token from this scanner.

###### **nextLine**
```java
public String nextLine()
```

