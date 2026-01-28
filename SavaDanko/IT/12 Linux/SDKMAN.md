	#linux 

---
`SDKMAN!` — это инструмент командной строки для управления версиями SDK (Software Development Kits).
Он делает установку, удаление, обновление и переключение между версиями инструментов максимально простыми.

SDKMAN поддерживает десятки технологий:
```bash
sdk list
```


###### ==Установка SDKMAN==
Просто выполни эту команду в терминале:
```bash
curl -s "https://get.sdkman.io" | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

`sdk version` - Display the current script and native versions of SDKMAN!

`sdk help`

`sdk list` - To get a listing of available Candidates

`sdk install <package>` - install

`sdk uninstall <package>` - uninstall

`sdk list <package>` - list versions

`sdk use <package>` - use version

`sdk defauls <package>` - chose to make a given version the default

`sdk current` - to see what is currently in use for all Candidates

`sdk upgrade`