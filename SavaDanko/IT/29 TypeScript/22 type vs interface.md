Оба варианта могут описывать объекты, функции, объединения (union), пересечения (intersection).
```ts
// type
type UserType = {
  id: number;
  name: string;
};

// interface
interface UserInterface {
  id: number;
  name: string;
}
```

В обоих случаях:
```ts
const user: UserType = { id: 1, name: "Alice" };
const user2: UserInterface = { id: 2, name: "Bob" };
```

###### **Отличия**
- `interface` расширяется через `extends`.
- `type` расширяется через `&` (intersection).
```ts
interface A { a: string; }
interface B extends A { b: number; }

type C = { a: string };
type D = C & { b: number };
```

Интерфейсы могут сливаться, `type` — нет.
```ts
interface Person {
  name: string;
}
interface Person {
  age: number;
}

const p: Person = { name: "Alice", age: 25 }; // ✅
```
`type` так не умеет — если объявить `type Person` дважды, будет ошибка.

`type` может описывать union и tuple, а `interface` — нет.
```ts
type ID = string | number; // ✅
type Point = [number, number]; // ✅

interface X {} // ❌ интерфейс так не может
```

`type` можно строить из выражений и условных типов, `interface` — нельзя.
```ts
type Status<T> = T extends string ? "ok" : "error";
type ReadonlyUser = Readonly<UserType>;
```
