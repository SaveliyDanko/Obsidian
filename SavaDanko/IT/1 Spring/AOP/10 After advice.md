`@After` — это тип advice в Spring AOP, который выполняется сразу после метода, даже если тот выбросил исключение.
- `@After` работает **аналогично `finally`** в `try/catch/finally`.
- Используется вместе с:
    - `@Aspect`
    - `@Pointcut` или `@After("execution(...)")`
- Не получает информацию о возвращаемом значении или исключении.  
    (Для этого существуют `@AfterReturning` и `@AfterThrowing`)

```java
@Aspect
@Component
public class LoggingAspect {

    @After("execution(* com.example.demo.PaymentService.processPayment(..))")
    public void afterAdvice(JoinPoint joinPoint) {
        System.out.println("[@After] Метод завершён: " + joinPoint.getSignature().getName());
    }
}
```
