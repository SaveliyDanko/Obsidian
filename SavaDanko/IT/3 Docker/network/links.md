Когда вы создаёте новый контейнер, вы можете указать Docker, что он должен быть связан* (linked) с другим контейнером.
Целевой контейнер должен быть запущен в момент создания нового контейнера.

Запуск контейнера с базой данных:
```bash
docker run -d --name importantData \
  --expose 3306 \
  dockerinaction/mysql_noauth \
  service mysql_noauth start
```

Запуск веб-приложения с ссылкой на базу данных:
```bash
docker run -d --name importantWebapp \
  --link importantData:db \
  dockerinaction/ch5_web \
  startapp.sh -db tcp://db:3306
```