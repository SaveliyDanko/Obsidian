В JavaScript существует 8 основных типов данных 
- number
```js
4
12.345
Infinity
-Infinity
NaN
```

- bigint
```js
// символ "n" в конце означает, что это BigInt 
const bigInt = 1234567890123456789012345678901234567890n;
```

- string
```js
let str = "Hello";
let str = 'Hello';

let phrase = `Обратные кавычки позволяют встраивать переменные ${str}`;
```

- boolean
```js
let checkedTrue = true;
let checkedFalse = false;

let isGreater = 4 > 1;
```

- null
```js
let age = null;
```

- undefined
```js
let age; 
alert(age) // выведет undefined

// -----

let age = 123;
age = undefined;
alert(age) // выведет undefined
```

- object
В объектах хранят коллекции данных или более сложные структуры.

- symbol
Используется для создания уникальных идентификаторов в объектах.