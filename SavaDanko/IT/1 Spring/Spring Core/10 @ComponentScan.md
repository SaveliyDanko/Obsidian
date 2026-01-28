---
tags:
  - review
sr-due: 2026-04-02
sr-interval: 65
sr-ease: 250
---

---
Чтобы Spring нашёл `@Component`, ты должен использовать **сканирование компонентов** — через `@ComponentScan` или автоматически через `@SpringBootApplication`.
```java
@Component
public class MyService {
    public void serve() {
        System.out.println("Service is running");
    }
}
```

И в конфигурации:
```java
@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {
}
```


