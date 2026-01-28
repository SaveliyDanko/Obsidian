---
tags:
  - review
sr-due: 2026-02-09
sr-interval: 38
sr-ease: 250
---

---
#### Docker CLI (Command Line Interface)
Это обычная команда `docker` в терминале. С ней ты напрямую управляешь контейнерами, образами, сетями и т. д.
```bash
docker run nginx                # Запускает контейнер с nginx
docker build -t myapp .        # Собирает образ из Dockerfile
docker ps                      # Показывает запущенные контейнеры
docker stop myapp              # Останавливает контейнер
```

#### Docker Compose
**Docker Compose** — это инструмент для управления многоконтейнерными приложениями. Вместо набора команд — ты описываешь всё приложение в YAML-файле (`docker-compose.yml`), а потом запускаешь одной командой.
```yaml
version: '3'
services:
  web:
    image: nginx
    ports:
      - "8080:80"
  redis:
    image: redis
```