`LoggerFactory` — это класс из библиотеки **SLF4J (Simple Logging Facade for Java)**, который используется для создания объектов логирования (`Logger`).  
Он предоставляет **унифицированный интерфейс** для различных библиотек логирования (например, Logback, Log4j).

`getLogger(Class<?> clazz)`
Возвращает логгер, привязанный к классу.
Рекомендуется использовать для получения логгера в классах.    
```java
Logger logger = LoggerFactory.getLogger(MyClass.class);
```
  
`getLogger(String name)`
Возвращает логгер с произвольным именем.  
Полезно при создании логгера на основе строки.    
```java
Logger logger = LoggerFactory.getLogger("CustomLogger");
```
  
`getILoggerFactory()`
Возвращает текущую реализацию логгера.
Используется для диагностики и настройки.    
```java
ILoggerFactory factory = LoggerFactory.getILoggerFactory();
System.out.println("Логгер: " + factory);
```
