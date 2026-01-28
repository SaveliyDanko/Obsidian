`Callable` — это интерфейс из пакета `java.util.concurrent`, предназначенный для запуска задач в отдельном потоке с возможностью вернуть результат и выбросить проверяемое исключение.
```java
@FunctionalInterface
public interface Callable<V> {
    V call() throws Exception;
}
```
