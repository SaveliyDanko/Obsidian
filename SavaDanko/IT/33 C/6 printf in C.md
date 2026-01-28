---
tags:
  - review
sr-due: 2026-02-08
sr-interval: 29
sr-ease: 250
---

---
`printf` в C — функция форматированного вывода, объявлена в `stdio.h`:
```c
#include <stdio.h>

printf("Hello!\n");
```
Она печатает строку формата, внутри которой могут быть placeholders — места, куда `printf` подставит значения из аргументов.

###### **Как выглядят placeholders**
Общий вид:
```
%[flags][width][.precision][length]specifier
```
Самое важное — `specifier` (тип значения), остальное опционально.

###### **Целые числа**
- `%d`
- `%i` — `int` (со знаком)
- `%u` — `unsigned int`
- `%ld` — `long`
- `%lld` — `long long`
```c
int a = -5;
unsigned int b = 10;
long long c = 1234567890123LL;

printf("a=%d b=%u c=%lld\n", a, b, c);
```

###### **Символ и строка**
- `%c` — `char` (печатает один символ)
- `%s` — C-строка `char*` (до `'\0'`)
```c
char ch = 'A';
char name[] = "Bob";

printf("ch=%c name=%s\n", ch, name);
```

###### **Вещественные**
- `%f` — `double`
- `%e` — экспоненциальная запись
```c
double x = 3.14159;
printf("x=%f x=%.2f x=%e\n", x, x, x);
```

###### **Width**
`%5d` — число минимум в 5 символов (слева пробелы):
```c
printf("|%5d|\n", 42);   // |   42|
```

###### **Precision**
Для `float/double`: количество знаков после точки:
```c
printf("%.3f\n", 1.23456);  // 1.235
```

Для строк `%s`: максимум символов:
```c
printf("%.4s\n", "abcdef"); // abcd
```
