###### **Условные типы (Conditional Types)**
Синтаксис:
```ts
T extends U ? X : Y
```
Читается так:  
Если `T` совместим с `U`, то результат `X`, иначе `Y`
```ts
type IsString<T> = T extends string ? "yes" : "no";

type A = IsString<string>; // "yes"
type B = IsString<number>; // "no"
```

###### **infer**
`infer` используется внутри условных типов, чтобы «вытащить» (вывести) тип из контекста.
```ts
type ElementType<T> = T extends (infer U)[] ? U : T;

type A = ElementType<string[]>;  // string
type B = ElementType<number[]>;  // number
type C = ElementType<boolean>;   // boolean
```
Здесь `infer U` позволяет захватить тип элементов массива.