**Проверка текущей версии git**
git --version

**Обновление git**
git --update

**Настройки имени пользователя git**
git config --global user.name “SavaDanko”

**Настройка электронной почты git**
git config --global user.email saveliydanko999@mail.ru

**Вывод текущих конфигураций git**
git config --list

**C помощью различных модификаций можно сохранять config на разных уровнях:**
--system (/etc/gitconfig)
--global
--local

**Сброс config параметров:**
git config --unset user.name
git config --unset user.email

**Клонирование репозитория:**
git clone  \<ref\>

**Создание git репозитория**
git init

**Просмотр текущего состояния репозитория git**
git status

**Добавление файлов в индекс (staging area)** (подготовка файлов перед commit)
git add “file.txt”
git add . (передача в staging area всего родительского каталога)

**Создание commit с записью изменений в репозиторий**
git commit -m \<message\>

**Просмотр информации о commit:**
Эта команда покажет подробности последнего коммита и список измененных файлов без показа содержимого изменений
``` shell
git show --name-only HEAD
```
Если вы хотите увидеть содержимое изменений, используйте просто `git show`:
``` shell
git show
```

**Просмотр истории изменений (коммитов)**
git log

**Информация о ветках проекта:**
git branch
git branch -v

**Создание новой ветки:**
git branch \<name\>

**Переименование ветки проекта:**
git branch -m “name”

**Переключение на другую ветку:**
git checkout \<name\>

Добавление удалённого репозитория: 
```bash
git remote add origin URL_ВАШЕГО_УДАЛЕННОГО_РЕПОЗИТОРИЯ
```

**Отправка изменений локального репозитория в удаленный, помеченный как источник**
git push origin master (main)

**Создание невой ветки и переключение на неё**
- git checkout -b feature/новая-функция

**Удаление локальной ветки**
* git branch -d <имя_ветки>:  Удаляет ветку, если она уже слита с веткой, от которой она была создана.
* git branch -D <имя_ветки>:  Удаляет ветку независимо от того, слита она или нет.

**Удаление удалённой ветки**
* git push origin --delete <имя_ветки>

**Слияние веток**
git merge feature/новая-функция

**Переименование файлов:**
git mv \<old\> \<new\>

**Игнорирование файлов:**
.gitignore (файл с файлами, которые не будут добавляться в staging area)

**Добавление автора в commit:**
git commit —author=”SaveliyDanko <saveliydanko@mail.ru>” --date=”…”

**Git не умеет работать с пустыми директориями**
Обычно в пустых директориях создают файл .gitkeep
