#java 

---
Prints formatted representations of objects to a text-output stream. This class implements all of the print methods found in `PrintStream`.

###### **PrintWriter**
```java
public PrintWriter(Writer out)
```
Creates a new PrintWriter, without automatic line flushing.

###### **PrintWriter**
```java
public PrintStream(OutputStream out,
							    boolean autoFlush,
								String encoding)
					            throws UnsupportedEncodingException
```
Creates a new print stream, with the specified OutputStream, line flushing, and character encoding.
###### **print**
```java
public void print(String s)
```
Prints a string.

###### **print**
```java
public void print(Object obj)
```
Prints an object.

###### **println**
```java
public void println(String x)
```
