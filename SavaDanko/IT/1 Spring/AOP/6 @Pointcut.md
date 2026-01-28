`@Pointcut` — это аннотация, которая **объявляет шаблон (условие)**, по которому Spring будет применять `advice`.

```java
@Aspect
@Component
public class LoggingAspect {

    // 1. Объявляем Pointcut
    @Pointcut("execution(* com.example.service.*.*(..))")
    public void allServiceMethods() {}

    // 2. Применяем его
    @Before("allServiceMethods()")
    public void beforeServiceMethod() {
        System.out.println("📍 Вызов метода сервиса");
    }
}
```

#### Комбинирование Pointcut
```java
@Pointcut("execution(* com.example.service.*.*(..))")
public void serviceMethods() {}

@Pointcut("@annotation(com.example.annotations.TrackTime)")
public void trackedMethods() {}

@Pointcut("serviceMethods() && trackedMethods()")
public void trackedServiceMethods() {}

@Around("trackedServiceMethods()")
public Object logAndTime(ProceedingJoinPoint pjp) throws Throwable {
    long start = System.currentTimeMillis();
    Object result = pjp.proceed();
    System.out.println("⏱ Время: " + (System.currentTimeMillis() - start) + "мс");
    return result;
}
```
