#js 

---
[Symbol](https://learn.javascript.ru/symbol)

---
#### Symbol в JavaScript
Symbol — это новый примитивный тип данных, введённый в ECMAScript 6. Символы используются для создания уникальных идентификаторов свойств объектов. Каждый символ гарантированно уникален, даже если они создаются с одинаковыми описаниями.

#### Создание Symbol
Символы создаются с помощью функции `Symbol()`:
```js
let id = Symbol();
```
Также можно добавить описание (идентификатор), чтобы облегчить отладку:
```js
let id = Symbol("description");
```
Важно: символы всегда уникальны. Даже если два символа созданы с одинаковыми описаниями, они будут разными:
```js
let id1 = Symbol("id");
let id2 = Symbol("id");
console.log(id1 === id2); // false
```

#### Использование Symbol как идентификаторов свойств объектов
Символы часто используются как уникальные ключи для свойств объектов. Это гарантирует отсутствие конфликтов имён, так как каждый символ уникален.
```js
let user = {
    name: "John"
};

let id = Symbol("id");
user[id] = 1;

console.log(user[id]); // 1
```
Свойства с ключами-символами не участвуют в обычных операциях перебора объектов, таких как `for..in`. Они скрыты от случайного доступа.

#### Символы в литералах объектов
Символы можно использовать как ключи в литералах объектов с помощью квадратных скобок:
```js
let id = Symbol("id");

let user = {
    name: "John",
    [id]: 123 // символ как ключ
};
```

#### Свойства Symbol не видны при переборе
Свойства, использующие символы как ключи, не выводятся при переборе объектов с помощью `for..in` или `Object.keys()`. Это делает символы полезными для создания скрытых свойств, которые нельзя случайно изменить или перезаписать:
```js
let id = Symbol("id");
let user = {
    name: "John",
    [id]: 123
};

for (let key in user) {
    console.log(key); // name, но нет id
}
```
Однако их можно получить, используя метод `Object.getOwnPropertySymbols()`:
```js
let symbols = Object.getOwnPropertySymbols(user);
console.log(symbols); // [Symbol(id)]
```

#### Глобальные символы
Иногда нужно, чтобы символы с одинаковым описанием были одинаковыми. Для этого существует глобальный реестр символов. Метод `Symbol.for()` ищет символ в глобальном реестре и, если он найден, возвращает его. Если символ не найден, он создаётся:
```js
let id1 = Symbol.for("id");
let id2 = Symbol.for("id");

console.log(id1 === id2); // true
```
Метод `Symbol.keyFor(sym)` возвращает строковое имя глобального символа:
```js
let sym = Symbol.for("name");
console.log(Symbol.keyFor(sym)); // "name"
```

#### Встроенные символы
JavaScript содержит множество встроенных символов, которые используются для управления поведением объектов. Примеры встроенных символов:
- `Symbol.iterator` — для итерации объектов. Используется в циклах `for..of`.
- `Symbol.toPrimitive` — для определения преобразования объекта в примитивное значение.
- `Symbol.toStringTag` — определяет, что будет возвращено методом `Object.prototype.toString`.

Пример использования `Symbol.toPrimitive`:
```js
let user = {
    name: "John",
    age: 30,
    [Symbol.toPrimitive](hint) {
        console.log(`hint: ${hint}`);
        return hint == "string" ? `{name: "${this.name}"}` : this.age;
    }
};

console.log(+user); // hint: number -> 30
console.log(`${user}`); // hint: string -> {name: "John"}
```

#### Сравнение Symbol и строк
Символы нельзя автоматически преобразовать в строки. При попытке конкатенации символа со строкой будет ошибка:
```js
let id = Symbol("id");
alert(id); // TypeError: Cannot convert a Symbol value to a string
```
Для явного преобразования можно использовать метод `.toString()`:
```js
let id = Symbol("id");
console.log(id.toString()); // Symbol(id)
```
Либо использовать `Symbol.description` для получения описания:
```js
let id = Symbol("id");
console.log(id.description); // "id"
```
