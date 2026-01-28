---
tags:
  - review
sr-due: 2026-04-18
sr-interval: 83
sr-ease: 250
---

---
**Namespaces** в Linux — это технология, которая изолирует ресурсы операционной системы между процессами. Когда Docker запускает контейнер, он создаёт для него отдельные namespaces, и процессы внутри контейнера не видят процессы и ресурсы других контейнеров или хоста.

`PID namespace` - Process identifiers and capabilities
`UTS namespace` - Host and domain name
`MNT namespace` - File system access and structure
`IPC namespace` - Process communication over shared memory
`NET namespace` - Network access and structure
`USR namespace` - User names and identifiers
`chroot()` - Controls the location of the file system root
`cgroups` - Resource protection