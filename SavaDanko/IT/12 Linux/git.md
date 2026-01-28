#linux 

---
**Стандартная установка через APT из официальных репозиториев Ubuntu**
```bash
sudo apt update
sudo apt install git
```

**Установка через официальный PPA (Personal Package Archive) от Git Core**
Этот способ позволяет установить последнюю стабильную версию Git, не дожидаясь её появления в стандартных репозиториях Ubuntu.
```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt update
sudo apt install git
```

**Сборка Git из исходников**
Если нужна конкретная версия или экспериментальная сборка.
```bash
sudo apt update
sudo apt install make libssl-dev libghc-zlib-dev libcurl4-gnutls-dev libexpat1-dev gettext unzip
wget https://github.com/git/git/archive/refs/tags/v2.45.2.zip -O git.zip  # Например, последняя версия на момент запроса
unzip git.zip
cd git-2.45.2
make prefix=/usr/local all
sudo make prefix=/usr/local install
```

**Проверка установленной версии**
После любого способа установки желательно проверить версию:
```bash
git --version
```
