---
tags:
  - review
sr-due: 2026-02-28
sr-interval: 37
sr-ease: 250
---

---
`scanf` $-$ Scan Formatted string
Accept character, string and numeric data from the user standart input $-$ Keyboard.

Scanf also use format specifiers like printf.
For example:
`%d` to accept input of integer type.
`%c` to accept input of character type
`%s` to accept a string
and so on...

```c
int var;
scanf("%d", &var);
```
While scanning the input, `scanf` needs to store that input data somewhere.
To store this input data, `scanf` needs to know the memory location of a variable.
`&` $-$ address of `var`