#linux 

---
#### ==Полезные ссылки==
**Темы и иконки для GNOME:**
[Gnome-look.org](https://www.gnome-look.org/browse/)
[Pling](https://www.pling.com)

**GNOME Extensions:**
[Gnome Extensions](https://extensions.gnome.org)

---
#### ==Установка расширений GNOME==
Устанавливаем **GNOME Tweaks** - инструмент для настройки внешнего вида и поведения системы.
```bash
sudo apt install gnome-tweaks
```

Устанавливаем **GNOME Extensions** - расширения для среды рабочего стола.
```bash
sudo apt install gnome-shell-extensions
sudo apt install chrome-gnome-shell
```

#### ==GNOME Extensions==
###### System monitor
Отображает информацию об использовании системы (процессор, память и т.д.) в верхней панели.

###### window-list
Добавляет нижнюю панель с классическим списком открытых окон.

###### Clipboard Indicator
Буфер обмена
[web site](https://github.com/Tudmotu/gnome-shell-extension-clipboard-indicator)

###### Dash to Dock
[web site](https://micheleg.github.io/dash-to-dock/index.html)

###### Compiz windows effect
[web site](https://github.com/hermes83/compiz-windows-effect)

###### Compiz alike magic lamp effect
[web site](https://github.com/hermes83/compiz-alike-magic-lamp-effect)

###### Burn My Windows
[web site](https://github.com/Schneegans/Burn-My-Windows)
Appartion
Glide
Focus
Doom
Broken Glass
Aura Grow
Matrix)

###### Desktop Widgets
[web site](https://gitlab.com/AndrewZaech/azclock)

###### Desktop Cube
[web site](https://github.com/Schneegans/Desktop-Cube)

###### Vitals
[web site](https://github.com/corecoding/Vitals)

#### ==Gnome Theme, Icons, Cursor==
**Создаем директории:**
```bash
mkdir ./.themes
mkdir ./.icons
```

Скачиваем темы, иконки и курсоры, затем распаковываем их в `./.themes` и `./.icons`
Курсоры тоже распаковываем в `./.icons`

Меняем тему и иконки в Gnome Tweaks:
- Shell
- Icons
- Cursor
- Legacy Applications (относится к визуальному оформлению устаревших приложений, использующих GTK2, а не современный GTK3/GTK4)

Приложения, которые скачаны с помощью snap или flatpak не подтянут иконки. Их нужно настроить вручную.
Создал скрипт, который выполняет копирование и настройку иконок и приложений.
