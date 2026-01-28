Jenkins — это один из самых популярных и мощных инструментов для организации процессов **CI/CD**. Он позволяет автоматизировать сборку, тестирование и деплой программного обеспечения, что значительно ускоряет и упрощает процесс разработки.

Создание образа Jenkins с помощью `docker compose`:
```yaml
version: '3.8'
services:
  jenkins:
    image: jenkins/jenkins:lts
    container_name: jenkins
    ports:
      - 8080:8080
      - 50000:50000
    volumes:
      - ./jenkins-data:/var/jenkins_home
      - /var/run/docker.sock:/var/run/docker.sock
```

В браузере переходим по ссылке:
```
http://<твой_сервер>:8080/
```

Получение пароля для первого входа:
```zsh
docker exec jenkins cat /var/jenkins_home/secrets/initialAdminPassword
```

---
```
username: savadanko
password: modula12345
```