Интерфейс `java.util.concurrent.Executor` — это фундаментальный строительный блок многопоточного программирования в Java. Он абстрагирует сам процесс запуска задач, позволяя разработчику разделить логику отправки задач на выполнение от деталей создания и управления потоками.
```java
@FunctionalInterface
public interface Executor {
    void execute(Runnable command);
}
```
