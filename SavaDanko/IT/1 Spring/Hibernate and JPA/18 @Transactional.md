---
tags:
  - review
sr-due: 2026-02-22
sr-interval: 69
sr-ease: 250
---

---
Аннотация `@Transactional` сообщает Spring:
Все операции внутри этого метода должны выполняться в одной транзакции. Если что-то пойдёт не так — откатить (rollback) все изменения.

То есть это граница атомарности:
- либо весь метод успешно завершается и все изменения фиксируются (`commit`)
- либо при ошибке всё отменяется (`rollback`).
```java
@Service
public class UserService {

    private final UserRepository repository;

    public UserService(UserRepository repository) {
        this.repository = repository;
    }

    @Transactional
    public void registerUser(User user) {
        repository.save(user);
        sendWelcomeEmail(user); // если тут упадёт исключение — insert отменится
    }
}
```

###### **Как работает под капотом**
Spring использует AOP (Aspect-Oriented Programming):
- При старте создаётся прокси-обёртка вокруг класса.
- Когда вызывается метод с `@Transactional`, прокси:
    1. Открывает транзакцию (через `EntityManager` / `DataSource`).
    2. Выполняет твой метод.
    3. При успехе делает `commit()`.
    4. При `RuntimeException` или `Error` — делает `rollback()`.
        

###### **Rollback — откат изменений**
По умолчанию Spring откатывает транзакцию, если выброшено неконтролируемое исключение (`RuntimeException` или `Error`).

###### **Параметры**

| Параметр        | Назначение                                             |
| --------------- | ------------------------------------------------------ |
| `readOnly`      | Оптимизация для запросов без изменений (SELECT)        |
| `propagation`   | Как новая транзакция ведёт себя относительно текущей   |
| `isolation`     | Уровень изоляции (READ_COMMITTED, SERIALIZABLE и т.д.) |
| `timeout`       | Лимит времени выполнения транзакции                    |
| `rollbackFor`   | Исключения, при которых делается rollback              |
| `noRollbackFor` | Исключения, при которых rollback не делается           |
