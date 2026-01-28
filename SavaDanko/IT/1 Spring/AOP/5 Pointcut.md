#### `execution(* ...)`
Это **pointcut-выражение**, определяющее, к каким методам применять аспект.
Формат:
```text
execution( modifiers-pattern? return-type-pattern declaring-type-pattern? method-name-pattern(parameters-pattern) throws-pattern?)
```

Примеры:
- `execution(* com.example.service.*.*(..))` — все методы во всех классах пакета `service`
- `execution(* get*(..))` — все методы, начинающиеся с `get`
- `execution(public void MyService.doSomething(..))` — конкретный метод