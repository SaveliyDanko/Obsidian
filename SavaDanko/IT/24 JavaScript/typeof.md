Оператор `typeof` возвращает тип аргумента.
У него есть две синтаксические формы:
```js
// Обычный синтаксис 
typeof 5 // выведет number

// Синтаксис, напоминающий вызов функции (встречается реже)
typeof(5) // выведет number
```

Если передается выражение, то нужно заключать его в скобки, т.к. typeof имеет более высокий приоритет, чем бинарные операторы:
```js
typeof 50 + " Квартир"; // Выведет "number Квартир"
typeof (50 + " Квартир"); // Выведет "string"`
```

Примеры
```js
typeof undefined; // "undefined" 

typeof 0; // "number"

typeof 10n; // "bigint"

typeof true; // "boolean"

typeof "foo"; // "string"

typeof Symbol("id"); // "symbol"

typeof Math; // "object"

typeof null; // "object"

typeof alert; // "function"
```

