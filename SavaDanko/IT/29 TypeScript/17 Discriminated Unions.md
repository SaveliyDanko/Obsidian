Discriminated unions — это приём, когда несколько типов объединяются в `union`, и у них есть общее свойство-дискриминатор с литеральным типом. TypeScript может использовать это свойство, чтобы сузить (narrowing) тип в разных ветках кода.

##### Пример
```ts
interface Circle {
  kind: "circle";
  radius: number;
}

interface Square {
  kind: "square";
  sideLength: number;
}

type Shape = Circle | Square;

function getArea(shape: Shape) {
  switch (shape.kind) {
    case "circle":
      return Math.PI * shape.radius ** 2; // shape: Circle
    case "square":
      return shape.sideLength ** 2;       // shape: Square
  }
}
```
Здесь `kind` — дискриминатор. TS по его значению понимает, какой именно тип передан.
