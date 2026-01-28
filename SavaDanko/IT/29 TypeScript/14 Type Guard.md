**Type Guard** — это специальная проверка в коде (например, `typeof`, `instanceof`, проверка на свойство), которая помогает TypeScript уточнить тип переменной.
```ts
function printId(id: string | number) {
  if (typeof id === "string") {
    console.log(id.toUpperCase()); // здесь id: string
  } else {
    console.log(id.toFixed());     // здесь id: number
  }
}
```