`apply()` — встроенный метод функций в JavaScript, который немедленно вызывает функцию, явно устанавливая `this` и передавая аргументы в виде массива или массивоподобного объекта.


###### **Синтаксис**
```js
func.apply(thisArg, [argsArray]);
```
- `thisArg` — значение для `this` внутри функции.
- `argsArray` — массив или массивоподобный объект (например, `arguments`, `NodeList`, `TypedArray`).
    
###### **Пример**
```js
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const user = { name: 'Alice' };

greet.apply(user, ['Hello', '!']);
// Hello, Alice!
```
Здесь:
- `this` внутри `greet` = `{ name: 'Alice' }`
- Аргументы переданы массивом.