[[5 Pointcut]]

---
#### `@Before` — перед вызовом метода
```java
@Before("execution(* com.example.service.*.*(..))")
public void beforeAdvice() {
    System.out.println("До метода");
}
```


#### `@AfterReturning` — после успешного выполнения
```java
@AfterReturning("execution(* com.example.service.*.*(..))")
public void afterReturningAdvice() {
    System.out.println("Метод успешно выполнен");
}
```

#### `@AfterThrowing` — если метод выбросил исключение
```java
@AfterThrowing("execution(* com.example.service.*.*(..))")
public void afterThrowingAdvice() {
    System.out.println("Метод выбросил исключение");
}
```

#### `@After` — после метода в любом случае
```java
@After("execution(* com.example.service.*.*(..))")
public void afterAdvice() {
    System.out.println("Метод завершён (независимо от результата)");
}
```

#### `@Around` — обёртка вокруг метода (до и после)
```java
@Around("execution(* com.example.service.*.*(..))")
public Object aroundAdvice(ProceedingJoinPoint joinPoint) throws Throwable {
    System.out.println("До вызова: " + joinPoint.getSignature().getName());
    Object result = joinPoint.proceed();
    System.out.println("После вызова: " + joinPoint.getSignature().getName());
    return result;
}
```
