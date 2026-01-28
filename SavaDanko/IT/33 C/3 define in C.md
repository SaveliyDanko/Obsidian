---
tags:
  - review
sr-due: 2026-02-07
sr-interval: 28
sr-ease: 250
---

---
`#define` в C — директива препроцессора, которая задаёт макрос: правило текстовой подстановки в коде до компиляции. Компилятор видит уже результат подстановки.

**define**
- define also names macro
```c
#define NAME value
```
- Job of preprocessor (not compiler) to replace NAME with value.
- Don't add semicolomn at the end.
- Choosing capital letters for NAME is good practice.

- Whatever inside double quoter `""` won't get replaced.
```c
#include <stdio.h>
#define value 89

int main() {
	printf("value is %d", value);
	return 0;
}
```

- We can use macros like functions
```c
#include <stdio.h>
#define add(x, y) (x+y)

int main() {
	printf("addition of two numbers: %d", add(3, 4));
	return 0;
}
```

- We can write multiple lines using `\`
```c
#include <stdio.h>

#define greater(x, y) if(x > y) \
        printf("%d is greater than %d", x, y); \
    else \
        printf("%d is lesser than %d", x, y);

int main() {
    greater(5, 6);
    return 0;
}
```

- First expansion then evaluation.
```c
#include <stdio.h>

#define add(x, y) x + y

int main() {
    printf("result of expression a * b + c is: %d", 5 * add(4, 3));
    return 0;
}
```
Answer is 23

- Some predefined macros like `__DATE__`, `__TIME__` can print current date and time.
```c
#include <stdio.h>

int main() {
    printf("Date: %s\n", __DATE__);
    printf("Time: %s\n", __TIME__);
    return 0;
}
```
