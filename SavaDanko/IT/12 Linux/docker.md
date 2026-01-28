#linux 

---
**Удаление старых версий**
Перед установкой Docker Engine необходимо удалить все конфликтующие пакеты.
Ваш дистрибутив Linux может предоставлять неофициальные пакеты Docker, которые могут конфликтовать с официальными пакетами, предоставляемыми Docker. Вы должны удалить эти пакеты перед установкой официальной версии Docker Engine.

Список неофициальных пакетов, которые необходимо удалить:
`docker.io`, `docker-compose`, `docker-compose-v2`, `docker-doc`, `podman-docker`
    
Кроме того, Docker Engine зависит от `containerd` и `runc`. Docker Engine включает эти зависимости в составе пакета `containerd.io`. Если вы ранее устанавливали `containerd` или `runc`, их также следует удалить, чтобы избежать конфликтов с версиями, которые поставляются вместе с Docker Engine.

Выполните следующую команду для удаления всех конфликтующих пакетов:
```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```
- `apt-get` может сообщить, что ни один из этих пакетов не установлен — это нормально, если вы ранее не устанавливали их вручную или через дистрибутив.
- При удалении Docker образы, контейнеры, тома и сети, находящиеся в каталоге `/var/lib/docker/`, не удаляются автоматически.

---
**Удаление Docker Engine**
Чтобы полностью удалить Docker Engine, CLI, containerd и Docker Compose, выполните следующую команду:
```bash
sudo apt-get purge docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin docker-ce-rootless-extras
```

Чтобы удалить все образы, контейнеры и тома вручную, выполните:
```bash
sudo rm -rf /var/lib/docker
sudo rm -rf /var/lib/containerd
```

Удаление списка репозиториев и ключей Docker:
```bash
sudo rm /etc/apt/sources.list.d/docker.list
sudo rm /etc/apt/keyrings/docker.asc
```
Любые изменённые вручную конфигурационные файлы (например, настройки Docker Daemon) нужно удалить самостоятельно.

---
**Методы установки Docker Engine**
Вы можете установить Docker Engine разными способами, в зависимости от ваших потребностей:
- Docker Engine входит в состав Docker Desktop для Linux.  
    Это самый простой и быстрый способ начать работу.    
- Установка Docker Engine из официального apt-репозитория Docker.  
    Рекомендуемый способ для большинства пользователей, так как позволяет получать обновления через стандартную систему пакетов.
- Ручная установка и самостоятельное управление обновлениями.  
    Полный контроль над процессом установки и обновления, но требует дополнительных действий со стороны пользователя.
- Использование установочного скрипта (convenience script).  
    Подходит только для тестовых и разработческих сред, не рекомендуется для рабочих серверов.
    
---
**Установка Docker Engine через apt-репозиторий**
Перед первой установкой Docker Engine на новом хосте необходимо добавить официальный репозиторий Docker. После этого вы сможете устанавливать и обновлять Docker через стандартный пакетный менеджер.

Добавление официального GPG-ключа Docker
```bash
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

Добавление репозитория Docker в список источников apt
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
```

Установка пакетов Docker
Чтобы установить последнюю версию Docker, выполните:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Проверка успешности установки
Запустите тестовый контейнер:
```bash
sudo docker run hello-world
```
Эта команда скачает тестовый образ и запустит контейнер, который выведет подтверждающее сообщение и завершит работу.

---
**Управление Docker без прав root**
Демон Docker привязывается к Unix-сокету, а не к TCP-порту. По умолчанию владельцем этого Unix-сокета является пользователь root, и другие пользователи могут обращаться к нему только через `sudo`. При этом сам демон Docker всегда работает от имени root.

Если вы не хотите каждый раз добавлять `sudo` перед командой `docker`, необходимо создать Unix-группу с именем docker и добавить в неё нужных пользователей. Когда демон Docker запускается, он создаёт Unix-сокет, доступный для членов группы docker.

На некоторых дистрибутивах Linux эта группа создаётся автоматически при установке Docker Engine через пакетный менеджер. В таком случае вручную создавать группу не требуется.

Чтобы создать группу docker и добавить в неё пользователя:
- Создайте группу `docker`:
    ```bash
    sudo groupadd docker
    ```
    
- Добавьте своего пользователя в группу `docker`:
    ```bash
    sudo usermod -aG docker $USER
    ```
    
- Выйдите из системы и войдите снова, чтобы обновились группы.  
Если вы работаете в виртуальной машине, может потребоваться перезапуск виртуалки.
    
- Чтобы применить изменения без выхода из системы, можно выполнить:
    ```bash
    newgrp docker
    ```
    
- Проверьте, что теперь можно запускать Docker-команды без `sudo`:
    ```bash
    docker run hello-world
    ```
Эта команда скачает тестовый образ и запустит контейнер, который выведет сообщение и завершит работу.

---
**Возможная ошибка после использования sudo ранее**
Если вы запускали команды Docker с `sudo` до добавления себя в группу, может появиться ошибка:
```
WARNING: Error loading config file: /home/user/.docker/config.json -
stat /home/user/.docker/config.json: permission denied
```
Это означает, что права доступа к каталогу `~/.docker/` некорректны из-за использования `sudo`.

Чтобы исправить это:
- Либо удалите каталог `.docker` (он будет создан автоматически при следующем запуске, но пользовательские настройки будут потеряны):    
    ```bash
    rm -rf ~/.docker
    ```
    
- Либо измените владельца и права доступа к каталогу:
    ```bash
    sudo chown "$USER":"$USER" /home/"$USER"/.docker -R
    sudo chmod g+rwx "$HOME/.docker" -R
    ```

---
**Настройка автозапуска Docker с помощью systemd**
Большинство современных дистрибутивов Linux используют systemd для управления службами, которые запускаются при старте системы.

На Debian и Ubuntu служба Docker по умолчанию стартует автоматически при загрузке системы.

Чтобы настроить автоматический запуск Docker и containerd при загрузке на других дистрибутивах Linux, использующих systemd, выполните следующие команды:
```bash
sudo systemctl enable docker.service
sudo systemctl enable containerd.service
```

---
**Отключение автозапуска**
Чтобы отключить автоматический запуск этих служб:
```bash
sudo systemctl disable docker.service
sudo systemctl disable containerd.service
```
