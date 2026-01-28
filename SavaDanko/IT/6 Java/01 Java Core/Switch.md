---
tags:
  - review
sr-due: 2026-06-16
sr-interval: 170
sr-ease: 290
---
---
```java
switch (выражение) {
    case значение1:
        // действия
        break;
    case значение2:
        // действия
        break;
    ...
    default:
        // действия по умолчанию
}
```

**switch-expression**
```java
String day = "MONDAY";

String result = switch (day) {
    case "MONDAY", "TUESDAY", "WEDNESDAY" -> "Рабочий день";
    case "SATURDAY", "SUNDAY" -> "Выходной";
    default -> "Неизвестный день";
};
```
