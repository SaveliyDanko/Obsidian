**Closure** — это функция, которая «замыкает» доступ к переменным из области видимости, в которой она была создана, даже после того, как эта область завершила выполнение.

Это ключевой механизм, на котором держатся многие вещи в JS: колбэки, обработчики событий, приватные данные, функциональное программирование.

###### **Как работает область видимости в JS**
- Каждая функция создаёт лексическое окружение (Lexical Environment) — внутреннюю структуру, где хранятся переменные и ссылки на внешнее окружение.
- Когда функция внутри другой функции использует переменные «снаружи», движок создаёт замыкание.
    
###### **Пример**
```js
function outer() {
  let count = 0;

  function inner() {
    count++;
    console.log(count);
  }

  return inner;
}

const fn = outer();
fn(); // 1
fn(); // 2
fn(); // 3
```
Что происходит:
1. `outer()` создаёт переменную `count` и возвращает `inner`.
2. `inner` помнит, где была создана, и держит ссылку на `count`.
3. Даже когда `outer` уже завершена, переменная `count` живёт, потому что на неё есть ссылка из замыкания.
    
###### **Приватные переменные**
```js
function createCounter() {
  let value = 0;
  return {
    inc: () => ++value,
    dec: () => --value,
    get: () => value
  };
}

const counter = createCounter();
console.log(counter.inc()); // 1
console.log(counter.get()); // 1
console.log(counter.value); // undefined
```
Переменная `value` недоступна напрямую.

###### **Генераторы функций**
```js
function makeAdder(a) {
  return function(b) {
    return a + b;
  };
}

const add5 = makeAdder(5);
console.log(add5(3)); // 8
```

###### **Обработчики событий**
```js
function setupButton(id) {
  let clicks = 0;
  document.getElementById(id).addEventListener('click', () => {
    clicks++;
    console.log(`Кликов: ${clicks}`);
  });
}
setupButton('myBtn');
```
Каждая кнопка будет хранить свой счётчик.
