Просмотр удаленных репозиториев:
```bash
git remote
```

Просмотр удаленных репозиториев и их адресов:
```bash
git remote -v
```

Добавление удаленного репозитория:
```bash
git remote add <shortname> <url>
git remote add pb https://github.com/paulboone/ticgit
```
`<shortname>` задаётся, чтобы можно было обращаться к репозиторию по короткому имени, вместо написания полного адреса
Ветки тоже становятся доступны под коротким именем `<shortname>/<branchname>`, например `origin/main`
После клонирования удалённого репозитория его `<shortname>` по умолчанию `origin`

Просмотр информации об удаленном репозитории
```bash
git remove show origin
```

Переименование удаленного репозитория:
```bash
git remote rename <old> <new>
```

Удаление удаленного репозитория:
```bash
git remote remove <name>
```

