**Mapped Types** — это механизм TypeScript, позволяющий создавать новые типы на основе существующих, перебирая их ключи (`keyof`) и трансформируя свойства.
```ts
type Person = {
  name: string;
  age: number;
};

// Mapped type: делаем все свойства обязательными и строковыми
type Stringified<T> = {
  [K in keyof T]: string;
};

type PersonStringified = Stringified<Person>;
// { name: string; age: string }
```
Здесь `[K in keyof T]` означает:
- перебираем все ключи типа `T`
- для каждого ключа указываем новый тип
