[Installation + Docs](https://github.com/pyenv/pyenv?tab=readme-ov-file#linuxunix)

---
**pyenv** — это инструмент, который позволяет:
- устанавливать разные версии Python
- легко переключаться между ними
- задавать версию Python глобально (для всей системы/пользователя),
- локально (для конкретного проекта — хранится в файле `.python-version`),
- или даже временно в рамках сессии

###### Установка версий Python
```bash
pyenv install --list         # показать доступные версии Python
pyenv install 3.11.9         # установить Python 3.11.9
pyenv install 3.12.4         # установить Python 3.12.4
```

###### Переключение версий
```bash
pyenv global 3.12.4          # глобальная версия (по умолчанию для пользователя)
pyenv local 3.11.9           # версия для текущего проекта (запишет .python-version)
pyenv shell 3.10.14          # версия только для текущей shell-сессии
```

###### Проверка
```bash
pyenv versions               # список установленных версий
pyenv version                # показать активную версию
which python                 # какой бинарь сейчас используется
python --version             # проверить версию
```

###### Удаление версий
```bash
pyenv uninstall 3.11.9
```
