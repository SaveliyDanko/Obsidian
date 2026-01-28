Удаление образа
```bash
docker rmi <image_id или image_name>
docker rmi $(docker images -f "dangling=true" -q)
```
> Образ должен не использоваться контейнером — иначе будет ошибка.

