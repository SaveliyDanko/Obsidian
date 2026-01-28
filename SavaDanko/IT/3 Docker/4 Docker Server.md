---
tags:
  - review
sr-due: 2026-02-01
sr-interval: 33
sr-ease: 250
---

---
#### Docker Server = Docker Daemon
Docker Server — это фоновый процесс, который принимает команды от клиента (CLI, Docker Compose и т. д.) и выполняет их: создаёт контейнеры, собирает образы, управляет сетью и томами.

Официальное название — `dockerd`.
```
Docker Client → Docker Daemon (Server) → Контейнеры, Сети, Образы, Тома
```
1. Docker Client (CLI) отправляет HTTP-запрос на сервер (`dockerd`).
2. Docker Server обрабатывает запрос
3. Результат возвращается клиенту (например, ID контейнера).
