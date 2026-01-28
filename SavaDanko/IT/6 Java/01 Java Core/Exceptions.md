#java 

---
**Исключение (`Exception`)** — это особое событие во время выполнения программы, которое нарушает нормальный ход выполнения.

##### Иерархия исключений
```
Throwable
├── Error (фатальные ошибки JVM)
└── Exception (рабочие ошибки, которые мы можем обработать)
    ├── Checked Exceptions (Проверяемые)
    └── Unchecked Exceptions (Непроверяемые = RuntimeException)
```
- **`Error`** — проблемы уровня JVM (OutOfMemoryError, StackOverflowError) → НЕ перехватываем.
- **`Exception`** — рабочие исключения:
    - **Checked Exception**: нужно обязательно обрабатывать (`IOException`, `SQLException`, и т.д.).
    - **Unchecked Exception**: можно не обрабатывать явно (`NullPointerException`, `IllegalArgumentException`, и т.д.).


##### Ключевые конструкции
- `try {}` — блок, где может возникнуть ошибка
- `catch(Exception e) {}` — перехват и обработка ошибки
- `finally {}` — выполняется **всегда**, даже если была ошибка
- `throw` — выброс исключения вручную
- `throws` — указание в сигнатуре метода, что он может выбросить исключение

##### Базовый `try-catch-finally`
```java
public class ExceptionExample {
    public static void main(String[] args) {
        try {
            int a = 10 / 0; // Деление на ноль → ArithmeticException
        } catch (ArithmeticException e) {
            System.out.println("Ошибка: " + e.getMessage());
        } finally {
            System.out.println("Блок finally всегда выполняется.");
        }
    }
}
```
