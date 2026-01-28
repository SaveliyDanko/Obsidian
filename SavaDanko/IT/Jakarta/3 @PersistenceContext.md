`@PersistenceContext` — это способ внедрить контейнерно-управляемый `EntityManager` (EM) в управляемый класс. Контейнер:
- создаёт/берёт нужный пул соединений (через ваш `persistence.xml` и JNDI-датасорсы)
- выдаёт вам прокси EM, привязанный к нужной persistence unit
- сам связывает EM с транзакцией и управляет его жизненным циклом
```java
@Path("/greetings")
@RequestScoped
public class GreetingResource {

  @PersistenceContext(unitName = "appPU")
  private EntityManager em;

  @POST @Transactional
  public Response create(Greeting g) {
    em.persist(g);
    return Response.status(201).entity(g).build();
  }
}
```
В контейнере не нужно вызывать `em.close()` — им управляет сервер.

#### Основные атрибуты `@PersistenceContext`
```java
@PersistenceContext(
  unitName = "appPU",
  type = PersistenceContextType.TRANSACTION,           // или EXTENDED
  synchronization = SynchronizationType.SYNCHRONIZED,  // или UNSYNCHRONIZED
  properties = { @PersistenceProperty(name="...", value="...") }
)
```
**`unitName`**
Имя `persistence-unit` из `META-INF/persistence.xml`. Если PU одна — можно опустить, но лучше указывать явно.

**`type`**
- `TRANSACTION` (по умолчанию) — контекст на транзакцию.  
    Ссылка на EM — прокси, который «приклеивается» к текущей JTA-транзакции (если она есть). Все изменения автоматически участвуют в коммите; без транзакции `persist/merge/remove` кинут `TransactionRequiredException`. Идеально для REST с `@Transactional`.
- `EXTENDED` — расширенный контекст, живущий дольше, чем одна транзакция.
    
**`synchronization`**
- `SYNCHRONIZED` (по умолчанию) — EM автоматически присоединяется к активной JTA-транзакции; flush происходит на коммите.
- `UNSYNCHRONIZED` — EM не присоединяется сам. Можно читать без риска «случайного flush», а для записи вручную звать `em.joinTransaction()`:
    
    ```java
    @PersistenceContext(unitName="appPU", synchronization = UNSYNCHRONIZED)
    EntityManager em;
    
    @Transactional
    void update(...) {
      // ... чтения
      em.joinTransaction();   // теперь EM участвует в коммите
      em.persist(entity);
    }
    ```
    

## `properties`

Редко нужно; передаёт вендорские настройки к конкретному контексту (обычно хватает настроек в `persistence.xml`).

# Как это работает с транзакциями

- В Jakarta EE/Payara вы, как правило, используете **JTA**.  
    Помечаете методы `@Transactional` (или EJB CMT). Контейнер открывает транзакцию → EM синхронизируется → `persist/merge/remove` попадают в коммит (EclipseLink сделает `flush` на коммите).
    
- Вне транзакции:
    
    - **чтение** (`find`, `createQuery` без `LOCK`) — разрешено,
        
    - **изменения** — вызовут `TransactionRequiredException` (кроме `EXTENDED`, где изменения копятся до явного join/коммита).
        
- `flush()` принудительно отправляет изменения в БД внутри транзакции; `clear()` отсоединяет все сущности; `detach()` — конкретную.
    

# Чем отличается от `@PersistenceUnit`

- `@PersistenceContext` → **`EntityManager`** (рабочий инструмент).
    
- `@PersistenceUnit` → **`EntityManagerFactory`** (фабрика EM), пригодится, когда вы хотите **создавать EM вручную** (например, в нестандартных сценариях/ресурс-локаторах). В обычном Jakarta EE приложении предпочтительнее `@PersistenceContext`.
    

# Где можно использовать

В **управляемых** классах: JAX-RS ресурсы, CDI-бины (`@ApplicationScoped`, `@RequestScoped`, `@Singleton` и т.п.), EJB. В «чистых» `new`-объектах (не управляемых контейнером) — **не сработает**.

# Потокобезопасность и жизненный цикл

- Инжектируемый EM — **не потокобезопасен**. Не складывайте его в `static`, не делитесь между потоками.
    
- В `TRANSACTION`-контексте используйте **короткоживущие** бины (обычно `@RequestScoped`/ресурсы).
    
- Никогда не зовите `em.close()` — контейнер закроет/освободит сам.
    

# Частые паттерны

**Репозиторий:**

```java
@ApplicationScoped
public class GreetingRepository {
  @PersistenceContext(unitName = "appPU")
  EntityManager em;

  public Optional<Greeting> find(long id) { return Optional.ofNullable(em.find(Greeting.class, id)); }

  @Transactional
  public Greeting save(Greeting g) { em.persist(g); return g; }
}
```

**EXTENDED c «мастер-формой»:**

```java
@Stateful
public class WizardBean {
  @PersistenceContext(unitName = "appPU", type = EXTENDED)
  EntityManager em;

  private Order draft;

  public void start() { draft = new Order(); em.persist(draft); } // managed между шагами

  @Transactional
  public void confirm() { /* изменения уже в контексте, коммит зафиксирует все */ }
}
```

# Типичные ошибки и как их избегать

- **Неверный `unitName`** → `No Persistence unit named ...`  
    Проверьте `persistence.xml` и точное имя.
    
- **Нет JTA-датасурса** / расхождение JNDI → ошибки при старте PU.  
    В `persistence.xml` задавайте корректные `<jta-data-source>`/`<non-jta-data-source>`, как вы уже сделали с `java:app/jdbc/...`.
    
- **Использование EM вне контейнера** → `null`/`Injection failed`.  
    Создавайте такие объекты через CDI/EJB, а не руками через `new`.
    
- **Ленивая загрузка после закрытия контекста** (LazyInitialization).  
    В REST не возвращайте «сырые» сущности с ленивыми связями; используйте DTO/прожекции/`JOIN FETCH` в пределах транзакции.
    
- **Долгоживущий EXTENDED без нужды** → утечки памяти/устаревшие данные.  
    Используйте только когда действительно нужен долгий разговор.
    

# Ваша связка (Payara Micro + EclipseLink)

- `@PersistenceContext(unitName="appPU")` берёт EM, привязанный к PU где:
    
    - `<jta-data-source>java:app/jdbc/PostgresDS</jta-data-source>`
        
    - `<non-jta-data-source>java:app/jdbc/PostgresDS__pm</non-jta-data-source>`
        
- С `@Transactional` (из `jakarta.transaction`) всё «едет из коробки»: EM синхронизируется, flush на коммите, SQL видно при включённом `eclipselink.logging.level.sql=FINE`.
    

Если хочешь, покажу, как проверить режим `UNSYNCHRONIZED` на маленьком примере (без автокоммита, с ручным `joinTransaction()`), или накину guideline по слою репозиториев/сервисов для твоих сущностей `LabWork/Person`.