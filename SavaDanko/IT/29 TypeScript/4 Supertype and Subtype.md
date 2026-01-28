In TypeScript, subtypes refer to types that are more specific or constrained versions of other types.

A subtype can be assigned to a variable of its supertype (or more general type) because it maintains all the properties and structure required by the supertype, but it may add more specific details.


```ts
type Person = {  
  name: string  
  age: number  
}  
  
type Student = {  
  name: string  
  age: number  
  school: string  
}  
  
const studentA: Student = {  
  name: "Apple Seed",  
  age: 19,  
  school: "Sydney University"  
}  
  
// Type Student is a subtype of type Person,  
// so it can be assigned to a variable of its supertype  
const personA: Person = studentA
```

###### Примитивы
```ts
type Super = string | number;
type Sub = string;

let a: Super = "hello";  // string подходит, так как string <: string|number
let b: Sub = "world";
b = a; // нельзя, потому что a может быть number
```
`string` — подтип `string|number`  
`string|number` — супертип для `string`

###### Объекты (структурная типизация)
В TS работает структурная типизация: тип считается подтипом, если он содержит минимум все свойства супертипа.
```ts
interface Person {
  name: string;
}

interface Employee extends Person {
  salary: number;
}

let p: Person = { name: "Alice" };
let e: Employee = { name: "Bob", salary: 1000 };

p = e; // Employee <: Person
e = p; // Person не <: Employee
```
`Employee` — подтип `Person`  
`Person` — супертип `Employee`
