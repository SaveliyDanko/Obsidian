---
tags:
  - review
sr-due: 2026-01-27
sr-interval: 3
sr-ease: 250
---

---
Intersection (`&`) создаёт новый тип, который должен одновременно удовлетворять всем объединённым типам.  

Пример:
```ts
type A = { id: number };
type B = { name: string };

type Person = A & B;

const user: Person = { id: 1, name: "Alice" }; // ✅ должен содержать и id, и name
```

###### **Совмещение разных интерфейсов/типов**
Альтернатива множественному наследованию классов.
```ts
interface Animal {
  eat(): void;
}

interface Pet {
  play(): void;
}

type PetAnimal = Animal & Pet;

const cat: PetAnimal = {
  eat: () => console.log("eating"),
  play: () => console.log("playing")
};
```

###### **Несовместимые типы дают `never`**
```ts
type A = string;
type B = number;

type Impossible = A & B; // never
```
Потому что значение не может быть одновременно строкой и числом.