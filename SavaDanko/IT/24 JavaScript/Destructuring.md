**Destructuring (деструктуризация)** в JavaScript — это способ «распаковки» значений из массивов или свойств объектов в отдельные переменные.


###### **Деструктуризация массива**
```js
const numbers = [10, 20, 30];

// Без деструктуризации
const a = numbers[0];
const b = numbers[1];

// С деструктуризацией
const [x, y] = numbers;

console.log(x); // 10
console.log(y); // 20
```

Можно пропускать элементы:
```js
const [first, , third] = [1, 2, 3];
console.log(first, third); // 1 3
```

Можно использовать значения по умолчанию:
```js
const [a = 5, b = 10] = [1];
console.log(a, b); // 1 10
```

###### **Деструктуризация объекта**
```js
const user = { name: "Alice", age: 25 };

// Без деструктуризации
const name1 = user.name;
const age1 = user.age;

// С деструктуризацией
const { name, age } = user;

console.log(name); // Alice
console.log(age);  // 25
```

Можно задавать псевдонимы (переименование):
```js
const { name: username, age: years } = user;
console.log(username); // Alice
console.log(years);    // 25
```

Значения по умолчанию:
```js
const { city = "Unknown" } = user;
console.log(city); // Unknown
```

###### **В параметрах функций**
```js
function greet({ name, age }) {
  console.log(`Привет, ${name}. Тебе ${age} лет.`);
}

greet({ name: "Bob", age: 30 });
// Привет, Bob. Тебе 30 лет.
```

###### **Деструктуризация + rest**
Можно собирать «остатки» в отдельную переменную:
```js
const [first, ...rest] = [1, 2, 3, 4];
console.log(first); // 1
console.log(rest);  // [2, 3, 4]

const { a, ...others } = { a: 1, b: 2, c: 3 };
console.log(a);      // 1
console.log(others); // { b: 2, c: 3 }
```

###### **Вложенная деструктуризация**
```js
const person = {
  name: "Eve",
  address: {
    city: "Paris",
    zip: "75000"
  }
};

const { address: { city } } = person;
console.log(city); // Paris
```
