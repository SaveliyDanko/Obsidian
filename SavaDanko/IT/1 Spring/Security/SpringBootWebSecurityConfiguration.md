---
tags:
  - review
sr-due: 2026-03-08
sr-interval: 71
sr-ease: 250
---

---
`SpringBootWebSecurityConfiguration` — это встроенная автоконфигурация Spring Boot, которая включает базовую защиту приложения, если ты не создал свою конфигурацию безопасности.
- Создаёт дефолтный `SecurityFilterChain`
- По умолчанию:
    - Все запросы требуют аутентификации
    - Включены form login и Basic Auth
- Активируется только если нет твоей конфигурации `SecurityFilterChain`
- Обеспечивает “безопасность из коробки”