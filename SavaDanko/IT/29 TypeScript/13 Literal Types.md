**Literal Types** в TypeScript — это типы, представляющие конкретные значения (`"hello"`, `42`, `true`).
```ts
let a: "on" | "off";   // может быть только "on" или "off"
let b: 1 | 2 | 3;      // только эти числа
let c: true | false;   // то же, что boolean
```
Обычно применяются в union для ограничения допустимых значений (например, `"left" | "right" | "center"`).
