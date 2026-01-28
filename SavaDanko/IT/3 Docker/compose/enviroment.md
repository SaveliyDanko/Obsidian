`environment` - Передаёт переменные окружения внутрь контейнера.

Пример:
```yaml
services:
  app:
    image: myapp
    environment:
      - APP_ENV=production
      - DEBUG=false
```
