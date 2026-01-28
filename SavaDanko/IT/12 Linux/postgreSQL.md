#linux 

---
```bash
sudo apt install postgresql postgresql-contrib -y
```
- `postgresql` — сервер и клиент
- `postgresql-contrib` — полезные расширения

Просмотр статуса службы:
```bash
sudo systemctl status postgresql
```
Остановить / запустить / перезапустить:
```bash
sudo systemctl stop postgresql
sudo systemctl start postgresql
sudo systemctl restart postgresql
```

PostgreSQL создаёт системного пользователя `postgres`, который может управлять БД через `psql`.
```bash
sudo --login --user postgres
psql
```
