**Optional Properties в функциях TS** — это параметры объекта, которые необязательны. Обозначаются `?` после имени свойства:
```ts
function printName(obj: { first: string; last?: string }) {
  console.log(obj.first);
  if (obj.last) console.log(obj.last.toUpperCase());
}
```
- `last?` → может быть `string` или `undefined`.
- При обращении нужно учитывать `undefined` (проверка или `?.`).
