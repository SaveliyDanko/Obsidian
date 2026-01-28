**Type Assertion** (утверждение типа) в TypeScript — это механизм, с помощью которого мы явно говорим компилятору: «Поверь мне, я знаю, что у этого значения именно такой тип».

Есть два варианта записи:
```ts
// через as
const input = document.getElementById("myInput") as HTMLInputElement;

// через <>
const input2 = <HTMLInputElement>document.getElementById("myInput");
```
Второй вариант (`<>`) нельзя использовать в `.tsx` (React), чтобы не путать с JSX.

###### **Пример: доступ к свойствам DOM**
```ts
const input = document.getElementById("username") as HTMLInputElement;
console.log(input.value); // ✅ компилятор "поверил", что это HTMLInputElement
```
Без `as` TypeScript думает, что `getElementById` возвращает `HTMLElement | null`, у которого может не быть свойства `.value`.

###### **Сужение типа**
Type Assertion может уточнить тип.
```ts
type Animal = { name: string };
type Dog = Animal & { bark: () => void };

const pet: Animal = { name: "Rex" };

// Утверждаем, что pet — это Dog
(pet as Dog).bark(); // ❌ ошибка в runtime, если bark реально не существует
```

###### **Двойное утверждение (as any as …)**
Иногда TypeScript не позволяет сделать слишком резкий каст — можно использовать промежуточный `any` или `unknown`.
```ts
const num = "123" as any as number; // опасный каст!
```