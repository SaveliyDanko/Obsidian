---
tags:
  - review
sr-due: 2026-04-21
sr-interval: 85
sr-ease: 250
---

---
`@Repository` в Spring — это аннотация для классов доступа к данным (DAO/репозиториев).
- Помечает класс как бин Spring (как `@Component`) → его можно внедрять через `@Autowired`/конструктор.
- Говорит Spring: это слой работы с БД → к нему подключается механизм перевода исключений (из `SQLException`/Hibernate-ошибок в `DataAccessException`).
