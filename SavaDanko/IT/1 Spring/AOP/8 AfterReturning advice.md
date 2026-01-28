`@AfterReturning` — это advice, который выполняется после успешного завершения метода, то есть если метод не выбросил исключение.
`@AfterReturning` позволяет получать `return` значение, но не изменять его

```java
@AfterReturning(pointcut = "...", returning = "result")
public void afterReturning(JoinPoint joinPoint, Object result) {
    // доступ к joinPoint и значению, которое вернул метод
}
```

`returning` - имя параметра, который примет возвращённое значение 
`Object result` - результат выполнения метода (можно кастовать к нужному типу)
