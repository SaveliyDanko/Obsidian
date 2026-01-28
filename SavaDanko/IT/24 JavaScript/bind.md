`bind()` — встроенный метод функций в JavaScript, который создаёт и возвращает новую функцию, у которой жёстко зафиксирован (`bound`) контекст `this` и (опционально) часть аргументов.  
В отличие от `call()` и `apply()`, `bind()` не вызывает функцию немедленно.

###### **Синтаксис**
```js
func.bind(thisArg, arg1, arg2, ...);
```
- `thisArg` — значение для `this` в новой функции.
- `arg1, arg2, ...` — аргументы, которые будут переданы в функцию по умолчанию при каждом вызове (частичное применение аргументов — partial application).
    


###### **Пример**
```js
function greet(greeting, punctuation) {
  console.log(`${greeting}, ${this.name}${punctuation}`);
}

const user = { name: 'Alice' };

const greetAlice = greet.bind(user, 'Hello');
greetAlice('!'); // Hello, Alice!
```
Здесь:
- `greet.bind(user, 'Hello')` вернёт новую функцию с `this = user` и первым аргументом `'Hello'`.
- Аргументы можно добавлять как при `bind`, так и при вызове.