Аннотация `@CrossOrigin` в Spring используется для настройки CORS (Cross-Origin Resource Sharing) — механизма, позволяющего веб-браузерам делать запросы к ресурсу, расположенному на другом домене. По умолчанию браузеры блокируют такие кросс-доменные запросы по соображениям безопасности, и `@CrossOrigin` — способ разрешить их в Spring-приложении.

###### **Пример:**
```java
@CrossOrigin(origins = "*", allowedHeaders = "*")
@GetMapping("/api/data")
public ResponseEntity<String> getData() {
    return ResponseEntity.ok("Hello from backend!");
}
```
- `origins = "*"`  
    Разрешает запросы с любых доменов. Это удобно для разработки, но опасно в проде, так как может открыть доступ к API кому угодно.
    
    Лучше указывать конкретные домены:
    ```java
    origins = {"https://example.com", "https://myapp.com"}
    ```
    
- `allowedHeaders = "*"`  
    Разрешает любые заголовки в запросах. Это важно, если фронтенд отправляет кастомные заголовки (например, `Authorization`, `X-Custom-Header` и т.п.).