На сервере, к которому хотим подключиться:
```bash
sudo apt update
sudo apt install openssh-server
```

Проверьте статус службы:
```bash
sudo systemctl status ssh
```

Если не запущен:
```bash
sudo systemctl enable ssh
sudo systemctl start ssh
```

Узнаем ip сервера
```bash
ip a
```

Проверьте настройки фаервола, если установлен `ufw`:
```bash
sudo ufw allow ssh
sudo ufw enable
sudo ufw status
```
Это откроет порт 22 для SSH.

На локальной машине:
```bash
ssh <имя_пользователя>@<ip-адрес_локального_пк>
```

Настройка подключения по ключам:
```bash
ssh-keygen -t rsa -b 4096 -f ~/.ssh/id_rsa_server_name -C "server_comment"
```

Копирование ключа на сервер:
```bash
ssh-copy-id -i ~/.ssh/id_rsa_server1.pub user@server1_ip
```

###### **Настройка файла** `~/.ssh/config`
Чтобы SSH понимал, какой ключ использовать для какого сервера, создайте или отредактируйте файл:
```bash
vim ~/.ssh/config
```

Пример содержимого:
```config
Host server1
    HostName 192.168.1.100
    User your_user_name
    IdentityFile ~/.ssh/id_rsa_server1

Host server2
    HostName 192.168.1.101
    User your_user_name
    IdentityFile ~/.ssh/id_rsa_server2
```

Теперь достаточно просто писать:
```bash
ssh server1
```