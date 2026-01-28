**Interface** в TypeScript — это способ описать структуру объекта (его свойства и их типы), а также контракты для классов.
```ts
interface User {
  id: number;
  name: string;
}

function printUser(user: User) {
  console.log(user.name);
}
```
- Можно расширять (`extends`) и объединять объявления.
- Подходит для описания форм объектов и API.
- Используется, когда нужно чётко задать «контракт» структуры.
