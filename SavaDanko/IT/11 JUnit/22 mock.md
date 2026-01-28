---
tags:
  - review
sr-due: 2026-02-12
sr-interval: 35
sr-ease: 230
---

---
Метод `mock()` в Mockito — это основной способ создать мок-объект, который имитирует поведение реального класса без выполнения его логики.

Он приходит из статического метода:
```java
import static org.mockito.Mockito.*;
```
и используется так:
```java
MyClass mockObject = mock(MyClass.class);
```


###### **Что mock() делает под капотом?**
Mockito создаёт динамический прокси, который:
- перехватывает ВСЕ вызовы методов
- по умолчанию возвращает `null / 0 / false / пустые коллекции`
- может быть запрограммирован через `when(...).thenReturn(...)`
- запоминает, какие методы ты вызвал (для `verify()`)
Это позволяет тестировать только логику твоего класса, без внешних зависимостей.

###### **Пример использования mock()**
Представь класс:
```java
public class UserRepository {
    public User findById(long id) {
        // лезет в базу
    }
}
```

В тесте:
```java
UserRepository repo = mock(UserRepository.class);

when(repo.findById(1L)).thenReturn(new User());

User u = repo.findById(1L);

verify(repo).findById(1L);
```

###### **Что можно делать с моками?**
Настраивать поведение
```java
when(mockedRepo.findAll()).thenReturn(List.of(new User()));
```

Заставлять бросать ошибки
```java
when(mockedRepo.save(any())).thenThrow(new RuntimeException());
```

Проверять вызовы
```java
verify(mockedRepo, times(1)).save(any());
```
