`keyof` — это оператор на уровне типов в TypeScript, который позволяет получить множество ключей объекта или интерфейса в виде объединения строковых литералов.
```ts
interface Person {
  name: string;
  age: number;
  isStudent: boolean;
}

type PersonKeys = keyof Person;
// "name" | "age" | "isStudent"
```

Теперь `PersonKeys` — это объединение строковых литералов, а значит, переменная такого типа может принимать только одно из этих значений:
```ts
let key: PersonKeys;

key = "name";       // ок
key = "age";        // ок
key = "isStudent";  // ок
key = "height";     // Ошибка: "height" не входит в "name" | "age" | "isStudent"
```

Можно получить ключи объекта через `typeof`:
```ts
const car = {
  brand: "Toyota",
  year: 2020,
  electric: false
};

type CarKeys = keyof typeof car;
// "brand" | "year" | "electric"
```

`keyof` часто используют вместе с индексацией типов:
```ts
interface Person {
  name: string;
  age: number;
}

type NameType = Person["name"]; // string
type AgeType = Person["age"];   // number
```

Объединим это с `keyof`:
```ts
type ValueOfPerson = Person[keyof Person];
// string | number
```
