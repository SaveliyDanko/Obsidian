**Type Predicate** — это способ написать свою функцию-защитник типа в TypeScript.  
Она сообщает компилятору: «если функция вернула `true`, то этот параметр имеет конкретный тип».

Синтаксис:
```ts
paramName is Type
```

#### Пример 1
```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };

function isFish(pet: Fish | Bird): pet is Fish {
  return (pet as Fish).swim !== undefined;
}

let pet: Fish | Bird = getSmallPet();

if (isFish(pet)) {
  pet.swim(); // pet: Fish
} else {
  pet.fly();  // pet: Bird
}
```

#### Пример 2: фильтрация массива
```ts
const zoo: (Fish | Bird)[] = [getSmallPet(), getSmallPet()];

// Массив только из рыб
const fishes: Fish[] = zoo.filter(isFish);
```
