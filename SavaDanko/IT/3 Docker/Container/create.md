`docker create` используется для создания контейнера, но без его запуска.

---
`-i, --interative` -  используется в командах `docker run` и `docker start` для того, чтобы оставить поток стандартного ввода (stdin) открытым даже после запуска контейнера. Это важно при работе с интерактивными программами, которые ожидают ввод от пользователя

`-t, --tty` - в Docker используется для выделения псевдотерминала (TTY) внутри контейнера. Он делает так, чтобы контейнер вел себя как обычный терминал, что полезно при интерактивной работе.

`-p, --publish` - publish a container's port(s) to the host

`--name` - assign a name to the container

`--cidfile` - write the container ID to the file

`--read-only` - mount the container's root filesystem as read only

`-e, --env` - используется, чтобы задать переменные окружения внутри контейнера.

`--restart` - restart policy to apply when a container exits
- `no` (по умолчанию) — никогда не перезапускать
- `on-failure` — перезапускать только при ошибке (не-ноль exit code)
- `on-failure:N` — то же, но максимум N попыток
- `always` — перезапускать всегда, независимо от причины
- `unless-stopped` — перезапускать всегда, если только не был остановлен вручную
Exponential backoff

`--rm` - automatically remove the container and its associated anonymous volumes when it exits

`--network host` при запуске Docker-контейнера отключает стандартную изоляцию сетевого стека контейнера и заставляет контейнер использовать сетевой стек хоста напрямую.

`--hostname, -h ` - Container host name

`--dns` - Set custom DNS servers

`--dns-search`
Если контейнер не может найти имя хоста напрямую, он автоматически добавляет указанный домен к этому имени и пробует снова.
Вместо того чтобы каждый раз писать полное имя, например:  
'myservice.dev.mycompany.com'. Вы можете писать просто 'myservice', а контейнер сам подставит домен поиска.

`--add-host` - позволяет вручную добавить в контейнер строку в файл `/etc/hosts`, то есть задать собственное соответствие между именем хоста и IP-адресом внутри контейнера.

