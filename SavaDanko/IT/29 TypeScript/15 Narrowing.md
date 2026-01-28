**Narrowing** — это процесс сужения объединённого типа до более конкретного подтипа на основе type guard'ов или других условий.

1. **typeof**:
```ts
function pad(value: string | number) {
  if (typeof value === "number") {
    return " ".repeat(value); // value: number
  }
  return value.trim();        // value: string
}
```

2. **instanceof**:
```ts
function logDate(d: Date | string) {
  if (d instanceof Date) {
    console.log(d.toISOString()); // d: Date
  } else {
    console.log(d.toUpperCase()); // d: string
  }
}
```

3. **Проверка свойства in**:
```ts
type Fish = { swim: () => void };
type Bird = { fly: () => void };

function move(animal: Fish | Bird) {
  if ("swim" in animal) {
    animal.swim(); // animal: Fish
  } else {
    animal.fly();  // animal: Bird
  }
}
```
