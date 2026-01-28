---
tags:
  - review
sr-due: 2026-06-04
sr-interval: 144
sr-ease: 270
---

---
**Array destructuring** — это способ распаковать значения из массива в отдельные переменные.
```ts
const arr = [10, 20, 30];

const [first, second] = arr;

console.log(first);  // 10
console.log(second); // 20
```
Значения распаковываются по позиции.

Можно пропускать элементы:
```ts
const [first, , third] = [1, 2, 3];

console.log(first); // 1
console.log(third); // 3
```
