#linux 

---
.deb package - архив, внутри внутри которого содержатся файлы программы и инструкции по установке. Эти файлы распаковываются в системую, например в /usr/bin, /etc, /opt...

После установки .deb package его необходимо установить в систему.
```bash
sudo apt install ./package_name.deb
```

После установки .deb package можно удалить. Содержимое из него уже "разложено по полочкам" в системе.
```bash
rm ./package_name.deb
```

Чтобы узнать имя пакета из .deb package:
```bash
dpkg-deb -f package_name.deb Package
```

[[dpkg]]
