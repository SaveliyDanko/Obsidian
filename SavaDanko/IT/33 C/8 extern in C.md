---
tags:
  - review
sr-due: 2026-02-19
sr-interval: 32
sr-ease: 250
---

---
`extern` в C используют, чтобы объявить глобальную переменную (или функцию), которая определена в другом файле. 

- **Определение (definition)** реально создаёт объект в памяти:
    ```c
    int counter = 0;   // это определение
    ```
    
- **Объявление (declaration)** сообщает компилятору, что объект существует где-то ещё: 
    ```c
    extern int counter; // это объявление, памяти не выделяет
    ```
Важно: `extern int counter;` можно писать много раз в разных `.c` — это нормально.  
Определение `int counter = 0;` должно быть ровно одно во всей программе.

###### **Типичная схема:** `.h` + `.c`
globals.h
```c
#ifndef GLOBALS_H
#define GLOBALS_H

extern int g_counter;     // объявление

#endif
```

globals.c
```c
#include "globals.h"

int g_counter = 0;        // единственное определение
```

main.c
```c
#include <stdio.h>
#include "globals.h"

int main(void) {
    g_counter++;
    printf("%d\n", g_counter);
}
```

###### `extern` **для функций**
Для функций `extern` обычно не пишут, потому что прототип функции по умолчанию имеет external linkage:
```c
// в .h
int add(int a, int b);  // это уже "extern" по смыслу
```

Но явно можно:
```c
extern int add(int a, int b);
```
