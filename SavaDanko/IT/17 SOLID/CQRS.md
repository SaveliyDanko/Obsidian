**CQRS (Command Query Responsibility Segregation)**
**Идея:** чтение и изменение данных — это разные виды нагрузки с разными требованиями. В CQRS мы разделяем:
- Командную сторону (Write/Command side) — принимает команды (Create/Update/Delete), проверяет инварианты домена, изменяет состояние агрегатов и публикует события.
- Запросную сторону (Read/Query side) — обслуживает запросы максимально быстро, читая из специально оптимизированной модели (денормализованные проекции, кэши, поисковые индексы и т.п.).

**Когда уместно**
- Нагрузка «много чтений, мало (но важных) записей», большие/сложные отчёты, разные SLA/масштабирование для чтения и записи.
- Сложные инварианты домена (агрегаты), разные модели данных и схемы для чтения/записи, микроcервисы.

**Плюсы**
- Независимое масштабирование чтения/записи.
- Упрощение кода каждой стороны: write — про инварианты, read — про быстрые запросы.

---
# Мини-архитектура примера

Для наглядности возьмём домен, близкий к вашим задачам — **LabWork**.

- **Write DB**: таблица `lab_work` (агрегат), таблица `outbox_event` (если пойдёте в Kafka/Дебезиум).
    
- **Read DB**: таблица `lab_work_view` (денорм проекция для быстрых GET).
    
- В демонстрации — один процесс Spring Boot. В проде обычно **раздельные сервисы и БД**.
    

---

# Реализация на Java / Spring Boot

> Зависимости: `spring-boot-starter-web`, `spring-boot-starter-data-jpa`, `spring-boot-starter-validation`, БД (H2/PostgreSQL). Для простоты — один datasource. В проде — два (write/read) + брокер.

## 1) Доменные классы и write-модель

```java
// domain/LabWork.java
package com.example.cqrs.domain;

import jakarta.persistence.*;
import jakarta.validation.constraints.NotBlank;
import jakarta.validation.constraints.NotNull;
import org.hibernate.annotations.CreationTimestamp;
import java.time.OffsetDateTime;

@Entity
@Table(name = "lab_work")
public class LabWork {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Version // оптимистическая блокировка для командной стороны
    private Long version;

    @NotBlank
    @Column(nullable = false)
    private String name;

    @Column(length = 2048)
    private String description;

    @NotNull
    @Column(nullable = false)
    private Integer minimalPoint;

    @CreationTimestamp
    @Column(nullable = false, updatable = false)
    private OffsetDateTime createdAt;

    protected LabWork() {}

    public LabWork(String name, String description, Integer minimalPoint) {
        if (minimalPoint <= 0) {
            throw new IllegalArgumentException("minimalPoint must be > 0");
        }
        this.name = name;
        this.description = description;
        this.minimalPoint = minimalPoint;
    }

    public void update(String name, String description, Integer minimalPoint) {
        if (minimalPoint != null && minimalPoint <= 0) {
            throw new IllegalArgumentException("minimalPoint must be > 0");
        }
        if (name != null && !name.isBlank()) this.name = name;
        if (description != null) this.description = description;
        if (minimalPoint != null) this.minimalPoint = minimalPoint;
    }

    // getters
    public Long getId() { return id; }
    public Long getVersion() { return version; }
    public String getName() { return name; }
    public String getDescription() { return description; }
    public Integer getMinimalPoint() { return minimalPoint; }
    public OffsetDateTime getCreatedAt() { return createdAt; }
}
```

```java
// domain/LabWorkRepository.java
package com.example.cqrs.domain;

import org.springframework.data.jpa.repository.JpaRepository;

public interface LabWorkRepository extends JpaRepository<LabWork, Long> {}
```

Команды (DTO), события и сервис:

```java
// app/commands/CreateLabWorkCommand.java
package com.example.cqrs.app.commands;

import jakarta.validation.constraints.NotBlank;
import jakarta.validation.constraints.NotNull;

public record CreateLabWorkCommand(
        @NotBlank String name,
        String description,
        @NotNull Integer minimalPoint
) {}
```

```java
// app/commands/UpdateLabWorkCommand.java
package com.example.cqrs.app.commands;

import jakarta.validation.constraints.NotNull;

public record UpdateLabWorkCommand(
        @NotNull Long id,
        String name,
        String description,
        Integer minimalPoint
) {}
```

```java
// app/events/LabWorkCreatedEvent.java
package com.example.cqrs.app.events;

public record LabWorkCreatedEvent(
        Long id,
        String name,
        String description,
        Integer minimalPoint
) {}
```

```java
// app/events/LabWorkUpdatedEvent.java
package com.example.cqrs.app.events;

public record LabWorkUpdatedEvent(
        Long id,
        String name,
        String description,
        Integer minimalPoint
) {}
```

```java
// app/LabWorkCommandService.java
package com.example.cqrs.app;

import com.example.cqrs.app.commands.CreateLabWorkCommand;
import com.example.cqrs.app.commands.UpdateLabWorkCommand;
import com.example.cqrs.app.events.LabWorkCreatedEvent;
import com.example.cqrs.app.events.LabWorkUpdatedEvent;
import com.example.cqrs.domain.LabWork;
import com.example.cqrs.domain.LabWorkRepository;
import org.springframework.context.ApplicationEventPublisher;
import org.springframework.stereotype.Service;
import org.springframework.transaction.annotation.Transactional;

@Service
public class LabWorkCommandService {

    private final LabWorkRepository repo;
    private final ApplicationEventPublisher events;

    public LabWorkCommandService(LabWorkRepository repo, ApplicationEventPublisher events) {
        this.repo = repo;
        this.events = events;
    }

    @Transactional
    public Long handle(CreateLabWorkCommand cmd) {
        var lw = new LabWork(cmd.name(), cmd.description(), cmd.minimalPoint());
        repo.save(lw);
        // публикуем доменное событие ПОСЛЕ коммита транзакции
        events.publishEvent(new LabWorkCreatedEvent(lw.getId(), lw.getName(), lw.getDescription(), lw.getMinimalPoint()));
        return lw.getId();
    }

    @Transactional
    public void handle(UpdateLabWorkCommand cmd) {
        var lw = repo.findById(cmd.id()).orElseThrow();
        lw.update(cmd.name(), cmd.description(), cmd.minimalPoint());
        // JPA dirty checking сохранит изменения
        events.publishEvent(new LabWorkUpdatedEvent(lw.getId(), lw.getName(), lw.getDescription(), lw.getMinimalPoint()));
    }
}
```

> В проде лучше публиковать события через **Transactional Outbox** (запись в outbox-таблицу в той же транзакции; затем отдельный паблишер/Дебезиум высылает в Kafka), а не напрямую `ApplicationEventPublisher`.

## 2) Read-модель (проекция)

```java
// query/LabWorkView.java
package com.example.cqrs.query;

import jakarta.persistence.*;

@Entity
@Table(name = "lab_work_view")
public class LabWorkView {
    @Id
    private Long id;

    @Column(nullable = false)
    private String name;

    @Column(length = 2048)
    private String description;

    @Column(nullable = false)
    private Integer minimalPoint;

    protected LabWorkView() {}
    public LabWorkView(Long id, String name, String description, Integer minimalPoint) {
        this.id = id; this.name = name; this.description = description; this.minimalPoint = minimalPoint;
    }

    public void update(String name, String description, Integer minimalPoint) {
        if (name != null) this.name = name;
        this.description = description;
        if (minimalPoint != null) this.minimalPoint = minimalPoint;
    }

    // getters
    public Long getId() { return id; }
    public String getName() { return name; }
    public String getDescription() { return description; }
    public Integer getMinimalPoint() { return minimalPoint; }
}
```

```java
// query/LabWorkViewRepository.java
package com.example.cqrs.query;

import org.springframework.data.jpa.repository.JpaRepository;
import java.util.List;

public interface LabWorkViewRepository extends JpaRepository<LabWorkView, Long> {
    List<LabWorkView> findByNameContainingIgnoreCase(String q);
}
```

**Проектор** — слушает доменные события и обновляет проекцию (read-таблицу):

```java
// query/LabWorkProjector.java
package com.example.cqrs.query;

import com.example.cqrs.app.events.LabWorkCreatedEvent;
import com.example.cqrs.app.events.LabWorkUpdatedEvent;
import org.springframework.stereotype.Component;
import org.springframework.transaction.event.TransactionPhase;
import org.springframework.transaction.event.TransactionalEventListener;

@Component
public class LabWorkProjector {

    private final LabWorkViewRepository repo;

    public LabWorkProjector(LabWorkViewRepository repo) {
        this.repo = repo;
    }

    @TransactionalEventListener(phase = TransactionPhase.AFTER_COMMIT)
    public void onCreated(LabWorkCreatedEvent e) {
        // idempotency: если событие придёт повторно — просто upsert
        if (repo.existsById(e.id())) return;
        repo.save(new LabWorkView(e.id(), e.name(), e.description(), e.minimalPoint()));
    }

    @TransactionalEventListener(phase = TransactionPhase.AFTER_COMMIT)
    public void onUpdated(LabWorkUpdatedEvent e) {
        var view = repo.findById(e.id()).orElseGet(() ->
                new LabWorkView(e.id(), e.name(), e.description(), e.minimalPoint()));
        view.update(e.name(), e.description(), e.minimalPoint());
        repo.save(view);
    }
}
```

## 3) Контроллеры: команды и запросы — раздельные эндпоинты

```java
// api/LabWorkCommandController.java
package com.example.cqrs.api;

import com.example.cqrs.app.LabWorkCommandService;
import com.example.cqrs.app.commands.CreateLabWorkCommand;
import com.example.cqrs.app.commands.UpdateLabWorkCommand;
import jakarta.validation.Valid;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/commands/labworks")
public class LabWorkCommandController {

    private final LabWorkCommandService service;

    public LabWorkCommandController(LabWorkCommandService service) {
        this.service = service;
    }

    @PostMapping
    public ResponseEntity<Long> create(@Valid @RequestBody CreateLabWorkCommand cmd) {
        Long id = service.handle(cmd);
        return ResponseEntity.ok(id);
    }

    @PutMapping("/{id}")
    public ResponseEntity<Void> update(@PathVariable Long id, @Valid @RequestBody UpdateLabWorkCommand body) {
        service.handle(new UpdateLabWorkCommand(id, body.name(), body.description(), body.minimalPoint()));
        return ResponseEntity.noContent().build();
    }
}
```

```java
// api/LabWorkQueryController.java
package com.example.cqrs.api;

import com.example.cqrs.query.LabWorkView;
import com.example.cqrs.query.LabWorkViewRepository;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/queries/labworks")
public class LabWorkQueryController {

    private final LabWorkViewRepository repo;

    public LabWorkQueryController(LabWorkViewRepository repo) {
        this.repo = repo;
    }

    @GetMapping
    public List<LabWorkView> list(@RequestParam(required = false) String q) {
        return (q == null || q.isBlank()) ? repo.findAll() : repo.findByNameContainingIgnoreCase(q);
    }

    @GetMapping("/{id}")
    public LabWorkView get(@PathVariable Long id) {
        return repo.findById(id).orElseThrow();
    }
}
```

## 4) Схема БД (минимум)

```sql
-- write side
CREATE TABLE lab_work (
  id BIGSERIAL PRIMARY KEY,
  version BIGINT NOT NULL,
  name VARCHAR(255) NOT NULL,
  description VARCHAR(2048),
  minimal_point INT NOT NULL,
  created_at TIMESTAMP WITH TIME ZONE NOT NULL
);

-- read side
CREATE TABLE lab_work_view (
  id BIGINT PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  description VARCHAR(2048),
  minimal_point INT NOT NULL
);
```

> В реальном проекте: разнести по разным БД/сервисам; добавить **outbox_event** с уникальным `event_id`, `aggregate_id`, `payload`, `type`, `created_at`, обработчик outbox → Kafka; на стороне чтения — **consumer** → projector (idempotent upsert).

---

# Практические советы по эксплуатации

- **Idempotency** проекций: обрабатывайте `event_id`/`aggregate_version` c дедупликацией.
    
- **Порядок событий:** гарантируйте порядок на уровне ключа агрегата (Kafka partition по `aggregateId`).
    
- **Согласованность UX:** возвращайте клиенту `202 Accepted` + ссылку на GET, пока проекция не обновилась; или «read-your-own-writes» через временный кэш/«inline read».
    
- **Версионирование событий:** добавляйте `schemaVersion` и поддерживайте backward/forward-совместимость.
    
- **Тестирование:** отдельно тестируйте write-инварианты и projector-логику (реплей набора событий).
    

---

# Что дальше

- Хотите — покажу версию с **Transactional Outbox + Kafka** (Debezium) и двумя разными datasource (write/read), или разнесём это на **два микросервиса**.
    
- Могу адаптировать под ваш домен (**Coordinates/Person/Discipline/LabWork**) и добавить сложные запросные проекции (например, фильтры/сортировки/агрегации для отчётов).