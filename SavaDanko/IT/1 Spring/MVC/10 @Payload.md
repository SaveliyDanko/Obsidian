Аннотация `@Payload` в Spring используется для указания, что аргумент метода должен быть заполнен из содержимого (тела) входящего сообщения — будь то HTTP, WebSocket, JMS, Kafka и т.д.

Spring пытается преобразовать тело сообщения в нужный Java-объект. Обычно это делается с помощью `MessageConverter` (например, Jackson JSON -> POJO).
###### **Пример:**
```java
@MessageMapping("/chat")
public void handleMessage(@Payload ChatMessage message) {
    System.out.println("Message text: " + message.getText());
}
```

Если клиент отправит JSON:
```json
{
  "text": "Hello",
  "sender": "user1"
}
```

Spring десериализует это в `ChatMessage`:
```java
public class ChatMessage {
    private String text;
    private String sender;
    // getters and setters
}
```
