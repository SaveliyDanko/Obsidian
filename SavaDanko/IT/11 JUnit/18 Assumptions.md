Assumptions в JUnit — это механизм, который позволяет условно пропускать тесты, если среда или данные не соответствуют ожидаемым условиям. Если "assumption" (предположение) не выполнено, тест не падает, а помечается как skipped (пропущенный).

###### **Зачем нужны assumptions?**
Assumptions используют, когда тест имеет смысл только при определённых условиях, например:
- тест должен запускаться только в production-профиле
- тест должен работать только при наличии переменной окружения
- тест актуален только для Windows или Linux
- тест должен выполняться только если база доступна
- ...

###### **Основные методы assumptions**
```
import static org.junit.jupiter.api.Assumptions.*;
```

###### `assumeTrue(condition)`
Если условие false → test skipped.
```java
assumeTrue(System.getProperty("os.name").contains("Windows"));
```

###### `assumeFalse(condition)`
```java
assumeFalse("ci".equals(System.getenv("ENV")));
```

###### `assumeNotNull(object...)`
Если хоть один объект null → тест пропущен.
```java
assumeNotNull(System.getenv("API_KEY"));
```