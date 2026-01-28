###### **`typeof` как оператор времени выполнения (runtime)**
Это обычный JavaScript-оператор, который возвращает строку с типом значения во время выполнения:
```ts
console.log(typeof "hello");  // "string"
console.log(typeof 123);      // "number"
console.log(typeof true);     // "boolean"
console.log(typeof {});       // "object"
console.log(typeof undefined);// "undefined"
console.log(typeof null);     // "object" (исторический баг в JS)
console.log(typeof (() => {})); // "function"
```
TypeScript умеет использовать такие проверки для сужения типов (`type narrowing`).
```ts
function printId(id: number | string) {
  if (typeof id === "string") {
    console.log(id.toUpperCase()); // здесь id: string
  } else {
    console.log(id); // здесь id: number
  }
}
```

###### **`typeof` как оператор времени компиляции (compile-time)**
В TypeScript можно использовать `typeof` в аннотациях типов, чтобы получить тип переменной или функции.
```ts
let message = "hello";
type MessageType = typeof message; 
// MessageType = string
```

Ещё пример — получение типа функции:
```ts
function greet(name: string) {
  return `Hello, ${name}`;
}

type GreetFn = typeof greet;
// GreetFn = (name: string) => string
```
Это удобно для повторного использования типов без дублирования.

###### **Комбинация с `keyof`**
Обычно `typeof` используют вместе с `keyof`, чтобы получить тип ключей объекта:
```ts
const person = {
  name: "Alice",
  age: 25
};

type Person = typeof person;
// { name: string; age: number; }

type PersonKeys = keyof typeof person;
// "name" | "age"
```
