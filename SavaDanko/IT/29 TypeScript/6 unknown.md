`unknown` — безопасная альтернатива `any`. Можно присвоить что угодно, но использовать — только после проверки.

Пример:
```ts
let value: unknown = "hello";

value.toUpperCase();  // ❌ ошибка
if (typeof value === "string") {
  console.log(value.toUpperCase()); // ✅ безопасно
}
```
- `unknown` — супертип для всех типов.