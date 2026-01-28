**JoinPoint** — это конкретная точка в процессе выполнения программы, в которой может быть выполнен дополнительный код из аспекта.
В Spring AOP `JoinPoint` — это объект, содержащий информацию о том месте, где сейчас выполняется аспект (метод, аргументы, объект и т.д.).


**Подключается автоматически в аргументах аспектов.**
```java
@Before("execution(* com.example.service.*.*(..))")
public void logMethodCall(JoinPoint joinPoint) {
    // можно использовать joinPoint.getSignature(), getArgs(), getTarget(), ...
}
```

| Метод            | Что возвращает                                        |
| ---------------- | ----------------------------------------------------- |
| `getSignature()` | Информация о методе: имя, параметры, возвращаемый тип |
| `getArgs()`      | Массив аргументов, переданных в метод                 |
| `getTarget()`    | Объект, на котором вызывается метод                   |
| `getThis()`      | Прокси-объект (обычно Spring-прокси)                  |
| `toString()`     | Читабельное представление точки соединения            |

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.UserService.*(..))")
    public void logBeforeMethod(JoinPoint joinPoint) {
        String methodName = joinPoint.getSignature().getName();
        Object[] args = joinPoint.getArgs();
    }
}
```

Используй `JoinPoint.getSignature()` → `MethodSignature`, чтобы получить более точную информацию:
```java
MethodSignature signature = (MethodSignature) joinPoint.getSignature();
Method method = signature.getMethod();
```
