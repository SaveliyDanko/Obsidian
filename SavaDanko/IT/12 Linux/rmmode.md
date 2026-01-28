#linux 

[[kernel]]
[[kernel module]]

---
`rmmod` — удаление модуля удаляет модуль из ядра.
```bash
sudo rmmod vfat
```
- Только если `Used by == 0` (`lsmod`)
- Может потребовать `modprobe -r`, если есть зависимости


    