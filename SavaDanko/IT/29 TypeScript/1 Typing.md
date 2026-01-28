---
tags:
  - review
sr-due: 2026-03-09
sr-interval: 83
sr-ease: 250
---

---
###### **Явная типизация (Explicit typing)**
Разработчик сам указывает тип переменной, параметра или возвращаемого значения.
```ts
let age: number = 25;       // явное указание
function sum(a: number, b: number): number {
  return a + b;
}
```

###### **Вводимая типизация (Type inference)**
TypeScript сам выводит тип из присвоенного значения или выражения.
```ts
let count = 10;         // TS выводит: number
let user = { id: 1, name: "Alice" }; // { id: number; name: string }

function multiply(a: number, b: number) {
  return a * b;   // TS выводит тип возврата: number
}
```

###### **Структурная типизация (Structural typing)**
В TS важна не номинальная совместимость типов, а структурная — совпадение формы объектов.
```ts
interface Person {
  name: string;
  age: number;
}

interface User {
  name: string;
  age: number;
}

let p: Person = { name: "Bob", age: 30 };

let u: User = p;
```
