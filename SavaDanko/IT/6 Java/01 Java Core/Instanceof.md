#java 

---
`instanceof` — это ключевое слово, которое возвращает `true`, если объект является экземпляром указанного класса или его подкласса, или реализует указанный интерфейс.

```java
object instanceof ClassName
```
- Возвращает `true` или `false`
- Безопасен: если объект `null` — всегда `false`

```java
String text = "Hello";

System.out.println(text instanceof String); // true
System.out.println(text instanceof Object); // true
System.out.println(text instanceof Number); // false
```
