Команда `docker exec` используется для запуска дополнительных процессов внутри уже запущенного контейнера. Это позволяет выполнять команды в контейнере без перезапуска или остановки.
```shell
docker exec [OPTIONS] container_name command [args...]
```

Подключение к контейнеру с помощью оболочки Bash:
```shell
docker exec -it my_container bash
```