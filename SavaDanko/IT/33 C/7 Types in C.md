---
tags:
  - review
sr-due: 2026-02-01
sr-interval: 24
sr-ease: 250
---

---
###### **Целочисленные типы (integer)**
- `signed` — могут быть отрицательные
- `unsigned` — только ≥ 0, но больший верхний предел

Основные
- `char` / `signed char` / `unsigned char`
- `short` / `unsigned short`
- `int` / `unsigned int`
- `long` / `unsigned long`
- `long long` / `unsigned long long`

Размеры зависят от платформы, но есть гарантии:
- `sizeof(char) == 1`
- `sizeof(short) ≤ sizeof(int) ≤ sizeof(long) ≤ sizeof(long long)`
- обычно: `int` 32 бита, `long` 64 на Linux x86_64, но `long` 32 на Windows x64 (LLP64)

###### **Вещественные типы (floating point)**
- `float` — обычно 32-битный
- `double` — обычно 64-битный
- `long double` — расширенный, размер/точность зависят от платформы

###### **Логический тип**
В C99+ есть:
```c
#include <stdbool.h>
bool ok = true;
```
Под капотом это целочисленный тип (`_Bool`), где 0 = false, 1 = true.

###### **Символьные**
- символ — это число, хранящее код (ASCII/UTF-8 байты и т.п.)
- `char` хранит один байт
- строка в C — это массив `char` с завершающим нулём `'\0'`:
```c
char s[] = "hi"; // {'h','i','\0'}
```

###### **Размеры: как узнавать правильно**
Не полагайся на “всегда 4 байта”. В C правильно так:
```c
printf("%zu\n", sizeof(int));
```
(`%zu` для `size_t`).
