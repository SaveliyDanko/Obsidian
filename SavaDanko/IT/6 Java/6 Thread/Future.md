Интерфейс `java.util.concurrent.Future` представляет собой механизм получения результата асинхронной или многопоточной операции в Java.
```java
public interface Future<V> {
    boolean cancel(boolean mayInterruptIfRunning);
    boolean isCancelled();
    boolean isDone();
    V get() throws InterruptedException, ExecutionException;
    V get(long timeout, TimeUnit unit) throws InterruptedException, ExecutionException, TimeoutException;
}
```


#### Пример простого использования с `Callable` и `ExecutorService`
```java
import java.util.concurrent.*;

public class FutureExample {
    public static void main(String[] args) throws Exception {
        ExecutorService executor = Executors.newSingleThreadExecutor();

        Callable<String> task = () -> {
            Thread.sleep(2000);
            return "Task completed";
        };

        Future<String> future = executor.submit(task);

        System.out.println("Waiting for result...");
        String result = future.get();  // Блокирующий вызов
        System.out.println("Result: " + result);

        executor.shutdown();
    }
}
```


| Метод                              | Описание                                                                          |
| ---------------------------------- | --------------------------------------------------------------------------------- |
| `cancel(boolean mayInterrupt)`     | Пытается отменить задачу. Если уже завершена — ничего не происходит.              |
| `isCancelled()`                    | Проверяет, была ли задача отменена.                                               |
| `isDone()`                         | Возвращает `true`, если задача завершена (успешно, с ошибкой или отменена).       |
| `get()`                            | Ожидает завершения задачи и возвращает результат. Может бросить `Exception`.      |
| `get(long timeout, TimeUnit unit)` | Ждёт указанное время, затем бросает `TimeoutException`, если задача не завершена. |
