#java 

---
An object that may be used to locate a file in a file system.

###### **of**
```java
static Path of(String first,
					  String... more)
```

###### **getFileSystem**
```java
FileSystem getFileSystem()
```
Returns the file system that created this object.

###### **isAbsolute**
```java
boolean isAbsolute()
```
Tells whether or not this path is absolute.

###### **getRoot**
```java
Path getRoot()
```
Returns the root component of this path as a `Path` object, or `null` if this path does not have a root component.
###### **getFileName**
```java
Path getFileName()
```
Returns the name of the file or directory denoted by this path as a `Path` object.

###### **getParent**
```java
Path getParent()
```
Returns the `parent path`, or `null` if this path does not have a parent.