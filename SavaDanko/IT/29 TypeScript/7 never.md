`never` — тип, у которого нет значений. Используется там, где выполнение невозможно.

Пример:
```ts
function fail(msg: string): never {
  throw new Error(msg);
}

function exhaustiveCheck(x: never): never {
  throw new Error("Unhandled case");
}
```
