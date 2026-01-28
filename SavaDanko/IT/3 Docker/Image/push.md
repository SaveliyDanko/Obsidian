`docker push` -  команда для отправки собранного образа в реестр.

Пример:
```bash
docker tag myapp myusername/myapp:latest
docker push myusername/myapp:latest
```
Ты публикуешь свой образ в реестре, и теперь его может скачать кто угодно (или только ты, если он приватный).
