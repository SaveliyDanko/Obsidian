---
tags:
  - review
sr-due: 2026-02-03
sr-interval: 30
sr-ease: 250
---

---
Считывает текст из символьного входного потока, буферизуя символы, чтобы обеспечить эффективное чтение отдельных символов, массивов символов и строк.
```java
public class BufferedReader extends Reader
```

В общем случае каждый запрос чтения, выполняемый через `Reader`, приводит к соответствующему запросу чтения из базового символьного или байтового потока. Поэтому рекомендуется оборачивать в `BufferedReader` любой `Reader`, операции `read()` которого могут быть дорогостоящими, например `FileReader` и `InputStreamReader`.
```java
BufferedReader in = new BufferedReader(new FileReader("foo.in"));
```

###### **readLine**
```java
public String readLine() throws IOException
```
Считывает строку текста.

###### **lines**
Возвращает `Stream`, элементы которого — строки, считываемые из данного `BufferedReader`.