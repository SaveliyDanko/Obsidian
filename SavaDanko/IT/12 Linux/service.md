#linux 

---
Команда service — это утилита для управления системными службами (демонами) на системах Linux. Она позволяет запускать, останавливать, перезапускать и проверять статус служб.

```zsh
sudo service <service_name> <command>
```

```zsh
sudo service ssh start         # Запуск SSH-сервиса
sudo service apache2 stop      # Остановка веб-сервера Apache
sudo service nginx restart     # Перезапуск Nginx
sudo service mysql status      # Проверка статуса MySQL
```

На современных системах рекомендуется напрямую использовать `systemctl`.

Список служб:
```zsh
service --status-all
```

