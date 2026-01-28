Аннотация `@MessageMapping` в Spring применяется в контексте Spring WebSocket / STOMP messaging и играет роль, аналогичную `@RequestMapping` в обычных HTTP-контроллерах. Она указывает, на какое сообщение (по какому пути) должен реагировать метод, когда клиент отправляет сообщение по STOMP-протоколу.
```java
@MessageMapping("/chat")
public void handleChatMessage(Message message) {
    // обработка сообщения
}
```
Когда клиент отправляет сообщение на `/app/chat` (по умолчанию префикс `/app` задается в конфигурации), этот метод будет вызван.

###### **Как это работает:**
1. Клиент подключается через WebSocket (обычно `/ws`).
2. Через STOMP он отправляет сообщение:
    ```javascript
    stompClient.send("/app/chat", {}, JSON.stringify({ text: "Hi!" }));
    ```
3. Метод `@MessageMapping("/chat")` на бэкенде обрабатывает это сообщение.
4. Метод может что-то вернуть — и сообщение будет доставлено подписчикам через `@SendTo`.
```java
@Controller
public class ChatController {

    @MessageMapping("/chat") // получает сообщение от клиента по адресу "/app/chat"
    @SendTo("/topic/messages") // отправляет результат всем подписанным на "/topic/messages"
    public ChatMessage processMessage(ChatMessage message) {
        message.setText("Server: " + message.getText());
        return message;
    }
}
```

Фронтенд:
```javascript
stompClient.subscribe("/topic/messages", function(msg) {
    const message = JSON.parse(msg.body);
    console.log(message.text);
});

stompClient.send("/app/chat", {}, JSON.stringify({ text: "Hello!" }));
```

###### **Конфигурация:**
```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void configureMessageBroker(MessageBrokerRegistry config) {
        config.enableSimpleBroker("/topic"); // выходящие сообщения
        config.setApplicationDestinationPrefixes("/app"); // входящие сообщения
    }

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/ws") // точка подключения WebSocket
                .setAllowedOriginPatterns("*")
                .withSockJS(); // поддержка SockJS
    }
}
```
