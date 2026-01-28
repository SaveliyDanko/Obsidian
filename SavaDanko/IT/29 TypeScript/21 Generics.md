Generics позволяют писать гибкий код*, который работает с разными типами, сохраняя при этом строгую типизацию.

Пример без generics:
```ts
function identity(arg: number): number {
  return arg;
}
```
Этот код работает только с числами. Но мы хотим, чтобы функция работала с любыми типами.

Используем `Generics`:
```ts
function identity<T>(arg: T): T {
  return arg;
}

const str = identity("hello"); // string
const num = identity(42);      // number
```

Здесь:
- `<T>` — обобщённый параметр типа.    
- TS автоматически выводит тип `T` из аргумента.

###### **Generics с массивами и интерфейсами**
```ts
function getFirst<T>(arr: T[]): T {
  return arr[0];
}

const firstNum = getFirst([1, 2, 3]);      // number
const firstStr = getFirst(["a", "b", "c"]); // string
```

Можно использовать в интерфейсах/классах:
```ts
interface Box<T> {
  value: T;
}

const stringBox: Box<string> = { value: "text" };
const numBox: Box<number> = { value: 123 };
```

###### **`extends` (ограничение generics)**
Иногда нужно, чтобы generic подходил только к определённому множеству типов.
```ts
function getLength<T extends { length: number }>(item: T): number {
  return item.length;
}

getLength("hello"); // ✅ 5
getLength([1, 2, 3]); // ✅ 3
getLength({ length: 10 }); // ✅ 10

getLength(42); // ❌ Ошибка: number не имеет свойства length
```

###### **Generic Conditions (`extends ? :`)**
TypeScript поддерживает условные типы:
```ts
type IsString<T> = T extends string ? "yes" : "no";

type A = IsString<string>; // "yes"
type B = IsString<number>; // "no"
```
