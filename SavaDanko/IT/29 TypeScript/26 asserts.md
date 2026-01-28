В TypeScript `asserts` используется для создания assertion functions, которые помогают компилятору сужать типы.
```ts
function assertIsString(value: unknown): asserts value is string {
  if (typeof value !== "string") {
    throw new Error("Not a string!");
  }
}

function printUpperCase(x: unknown) {
  assertIsString(x);
  // после вызова выше TS знает, что x: string
  console.log(x.toUpperCase());
}
```
Здесь `asserts value is string` сообщает TS, что после успешного вызова `assertIsString` переменная `value` точно `string`.