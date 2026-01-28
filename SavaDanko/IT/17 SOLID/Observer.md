---
tags:
  - review
sr-due: 2026-03-26
sr-interval: 107
sr-ease: 270
---

---
_todo:_ ассинхронная версия

---
**Идея:** у нас есть объект-издатель (_Subject_), который хранит состояние. Есть подписчики (_Observers_), которым нужно узнавать об изменениях этого состояния. Издатель не знает деталей подписчиков — он лишь уведомляет их через общий интерфейс. Это снижает связанность и упрощает расширение системы.

###### **Ключевые детали дизайна**
- Push vs Pull:
    - Push — издатель передаёт готовые данные в аргументах `update(event)`.
    - Pull — издатель лишь сигналит об изменении, а наблюдатель сам читает нужное из издателя.
- Синхронность: по умолчанию вызовы наблюдателей синхронные; при необходимости делайте диспетчеризацию в пул потоков.
- Управление жизненным циклом: важно уметь отписываться, иначе возможны утечки памяти.
- Гранулярность событий: иногда имеет смысл передавать тип события/дифф, а не «всё состояние целиком».
- Стандартные варианты в Java: старые `java.util.Observable/Observer` устарели. Современные варианты — `PropertyChangeSupport`/`PropertyChangeListener`, `java.beans` (просто и синхронно) или реактивное `java.util.concurrent.Flow` (асинхронные стримы).

###### **Классическая реализация**
Ниже — простой пример «Метеостанция → дисплеи/логгер». Используем push-модель и потокобезопасные структуры.
```java
import java.util.List;
import java.util.Objects;
import java.util.Optional;
import java.util.concurrent.CopyOnWriteArrayList;

// Событие (пример)
public record Event(String info) { }

// Наблюдаемая сущность
public interface Subject<E> {
    void addObserver(Observer<E> observer);
    void removeObserver(Observer<E> observer);
    void trigger(E event);
}

// Наблюдатель
@FunctionalInterface
public interface Observer<E> {
    void onEvent(E event);
}

// Конкретный субъект
public class SubjectA<E> implements Subject<E> {
    private final List<Observer<E>> observers = new CopyOnWriteArrayList<>();

    @Override
    public void addObserver(Observer<E> observer) {
        if (!observers.contains(observer)) {
            observers.add(observer);
        }
    }

    @Override
    public void removeObserver(Observer<E> observer) {
        observers.remove(observer);
    }

    @Override
    public void trigger(E event) {
        lastEvent = event;
        for (Observer<E> o : observers) {
            try {
                o.onEvent(event);
            } catch (RuntimeException ex) {
                // логируйте; важно не "ронять" рассылку для остальных
                ex.printStackTrace();
            }
        }
    }
}

// Конкретный наблюдатель
public class ObserverA implements Observer<Event> {
    private String info;

    public String getInfo() {
        return info;
    }

    @Override
    public void onEvent(Event event) {
        this.info = event.info();
        System.out.println("Update " + info);
    }
}

// Демонстрация
public class Main {
    public static void main(String[] args) throws Exception {
        Subject<Event> subject = new SubjectA<>();
        ObserverA observer = new ObserverA();
        
        subject.addObserver(observer);
        subject.trigger(new Event("event1"));
        subject.trigger(new Event("event2"));
    }
}

```