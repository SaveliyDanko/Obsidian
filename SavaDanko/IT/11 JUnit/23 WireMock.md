---
tags:
  - review
sr-due: 2026-04-16
sr-interval: 82
sr-ease: 250
---

---
**WireMock** — это инструмент для имитации (мокирования) HTTP-сервисов. Он позволяет создавать заглушки для внешних API и веб-сервисов, чтобы тестировать приложения в изоляции. WireMock запускает реальный HTTP-сервер, который имитирует поведение реального сервиса, но полностью контролируется вами.

###### **Ключевые возможности**
###### 1. Запись и воспроизведение
WireMock может записывать запросы к реальному сервису и сохранять их как "стабы" для последующего использования:
```java
wireMockServer.startRecording("http://real-api.com");
// Выполняем запросы к реальному API
wireMockServer.stopRecording();
```

###### 2. Гибкое сопоставление запросов
Можно настраивать правила для разных типов запросов:
```java
stubFor(get(urlEqualTo("/api/users"))
    .willReturn(aResponse()
        .withStatus(200)
        .withHeader("Content-Type", "application/json")
        .withBody("{\"users\": [\"John\", \"Jane\"]}")));
```

###### 3. Динамические ответы
Можно генерировать ответы на основе запросов:
```java
stubFor(post(urlEqualTo("/api/data"))
    .willReturn(aResponse()
        .withTransformers("response-template")
        .withTransformerParameter("body", "Hello {{request.query.name}}!")));
```

###### 4. Задержки и таймауты
Имитация медленных ответов:
```java
stubFor(get(urlEqualTo("/slow-api"))
    .willReturn(aResponse()
        .withFixedDelay(5000) // 5 секунд задержки
        .withStatus(200)));
```

###### 5. Верификация запросов
Проверка, какие запросы были отправлены:
```java
verify(exactly(1), postRequestedFor(urlEqualTo("/api/orders")));
```

###### **Режимы работы**
###### Стандартный режим
Запуск как отдельного сервера (Java):
```bash
java -jar wiremock-standalone.jar --port 8080
```

###### Встроенный режим
Использование в JUnit тестах:
```java
@Rule
public WireMockRule wireMockRule = new WireMockRule(8080);

@Test
public void testApiClient() {
    // Настройка стабов
    stubFor(get(urlEqualTo("/test"))
        .willReturn(aResponse().withBody("Hello")));
    
    // Тестирование клиента
    ApiClient client = new ApiClient("http://localhost:8080");
    String response = client.get("/test");
    
    assertEquals("Hello", response);
    verify(getRequestedFor(urlEqualTo("/test")));
}
```

###### Docker контейнер
```bash
docker run -it --rm -p 8080:8080 wiremock/wiremock
```

###### **Примеры использования**
###### 1. Тестирование REST клиента
```java
public class UserServiceTest {
    
    @Rule
    public WireMockRule wireMock = new WireMockRule();
    
    @Test
    public void shouldFetchUsers() {
        // Настраиваем мок
        stubFor(get(urlEqualTo("/users"))
            .willReturn(aResponse()
                .withHeader("Content-Type", "application/json")
                .withBody("[{\"id\": 1, \"name\": \"John\"}]")));
        
        // Тестируем
        UserService service = new UserService("http://localhost:8080");
        List<User> users = service.getUsers();
        
        assertEquals(1, users.size());
        assertEquals("John", users.get(0).getName());
    }
}
```

###### 2. Имитация ошибок
```java
// Имитация 500 ошибки
stubFor(get(urlEqualTo("/error"))
    .willReturn(aResponse()
        .withStatus(500)
        .withBody("Internal Server Error")));

// Имитация таймаута
stubFor(get(urlEqualTo("/timeout"))
    .willReturn(aResponse()
        .withFixedDelay(10000)
        .withStatus(200)));
```

###### 3. Сценарий с несколькими ответами
```java
// Первый запрос возвращает один ответ, второй - другой
stubFor(get(urlEqualTo("/multi"))
    .inScenario("Retry Scenario")
    .whenScenarioStateIs(Scenario.STARTED)
    .willReturn(aResponse().withStatus(500))
    .willSetStateTo("Failed"));

stubFor(get(urlEqualTo("/multi"))
    .inScenario("Retry Scenario")
    .whenScenarioStateIs("Failed")
    .willReturn(aResponse().withStatus(200)));
```
