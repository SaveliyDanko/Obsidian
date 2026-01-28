#linux 

[[kernel module]]
[[kernel]]

---
`modprobe` — рекомендуемая команда: автоматически загружает модуль и его зависимости.
```bash
sudo modprobe vfat
```
- Ищет модуль в `/lib/modules/$(uname -r)/`
- Загружает нужные зависимости
- Использует конфигурации из `/etc/modprobe.d/*.conf`

