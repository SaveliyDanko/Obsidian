**Utility Types** — это встроенные вспомогательные типы в TypeScript, которые упрощают работу с объектами, массивами и другими структурами.  
Они в основном построены на Mapped Types + Generics + Conditional Types.

###### **Основные Utility Types**
`Partial<T>`
Делает все свойства необязательными.
```ts
interface User {
  id: number;
  name: string;
}

type PartialUser = Partial<User>;
// { id?: number; name?: string }
```

`Required<T>`
Делает все свойства обязательными.
```ts
interface User {
  id?: number;
  name?: string;
}

type FullUser = Required<User>;
// { id: number; name: string }
```

`Readonly<T>`
Делает свойства только для чтения.
```ts
interface User {
  id: number;
  name: string;
}

type ReadonlyUser = Readonly<User>;
// { readonly id: number; readonly name: string }
```

`Pick<T, K>`
Берёт только выбранные свойства.
```ts
interface User {
  id: number;
  name: string;
  age: number;
}

type UserPreview = Pick<User, "id" | "name">;
// { id: number; name: string }
```

`Omit<T, K>`
Убирает выбранные свойства.
```ts
type UserWithoutAge = Omit<User, "age">;
// { id: number; name: string }
```

`Record<K, T>`
Создаёт объект с ключами `K` и значениями `T`.
```ts
type Roles = "admin" | "user";

type RolePermissions = Record<Roles, boolean>;
// { admin: boolean; user: boolean }
```

`Exclude<T, U>`
Удаляет из `T` все типы, которые входят в `U`.
```ts
type T = Exclude<"a" | "b" | "c", "a">;
// "b" | "c"
```

`Extract<T, U>`
Берёт только пересечение типов.
```ts
type T = Extract<"a" | "b" | "c", "a" | "d">;
// "a"
```

`NonNullable<T>`
Убирает `null` и `undefined`.
```ts
type T = NonNullable<string | number | null | undefined>;
// string | number
```

`ReturnType<T>`
Берёт тип возвращаемого значения функции.
```ts
function getUser() {
  return { id: 1, name: "Alice" };
}

type User = ReturnType<typeof getUser>;
// { id: number; name: string }
```

`Parameters<T>`
Берёт типы параметров функции как tuple.
```ts
function greet(name: string, age: number) {}

type Params = Parameters<typeof greet>;
// [name: string, age: number]
```

`ConstructorParameters<T>`
То же самое, но для конструкторов.
```ts
class User {
  constructor(public id: number, public name: string) {}
}

type Params = ConstructorParameters<typeof User>;
// [id: number, name: string]
```
