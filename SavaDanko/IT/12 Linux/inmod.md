#linux 

[[kernel]]
[[kernel module]]
[[modprobe]]

---
`insmod` — ручная загрузка: загружает один конкретный `.ko` файл.
```bash
sudo insmod /lib/modules/$(uname -r)/kernel/fs/vfat/vfat.ko
```

⚠️ Не подгружает зависимости — ты сам должен загружать всё вручную!

➕ Полезно для разработчиков, отладки или кастомных модулей.