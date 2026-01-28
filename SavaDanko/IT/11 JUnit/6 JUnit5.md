---
tags:
  - review
sr-due: 2026-03-17
sr-interval: 65
sr-ease: 250
---

---
**JUnit5** - фреймворк для модульного тестирования в Java.
**JUnit Jupiter API:** программный интерфейс для написания тестов.
**JUnit5 Engine:** движок, выполняющий тесты на платформе JUnit 5.
**JUnit Launcher:** компонент для запуска тестов с использованием разных движков.

##### **Использование JUnit Launcher API:**
```java
import org.junit.platform.launcher.*;
import org.junit.platform.launcher.core.*;

public class CustomLauncher {
    public static void main(String[] args) {
        LauncherDiscoveryRequest request = LauncherDiscoveryRequestBuilder.request()
            .selectors(DiscoverySelectors.selectClass("SimpleTest"))
            .build();

        Launcher launcher = LauncherFactory.create();
        launcher.execute(request);
    }
}
```

###### **Поток выполнения:**
1. JUnit Platform вызывает Launcher.
2. Launcher выбирает движок (например, JUnit5 Engine).
3. Движок выполняет тесты, написанные с использованием JUnit Jupiter API.
4. Результаты передаются на платформу и выводятся в консоль или файл.