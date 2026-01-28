#js 

---
###### Default export
- У файла может быть только один `export default`.
- Имя при импорте можно придумать любое — оно не обязано совпадать с именем в файле.

`example.js`
```js
export default function sayHello() {
  console.log("Hello!");
}
```

`main.js`
```js
import greet from './example.js'; // можно назвать как угодно
greet(); // Hello!
```
Обычно используют для главного объекта/функции/класса, который «ассоциирован» с файлом.

###### **Named export**
- Можно экспортировать сколько угодно переменных, функций, классов.
- При импорте имена должны совпадать (в фигурных скобках).

`math.js`
```js
export const PI = 3.14;
export function sum(a, b) {
  return a + b;
}
export function mul(a, b) {
  return a * b;
}
```

`main.js`
```js
import { PI, sum, mul } from './math.js';

console.log(PI);        // 3.14
console.log(sum(2, 3)); // 5
```
Можно переименовать при импорте:
```js
import { sum as add } from './math.js';
console.log(add(1, 2)); // 3
```

###### Смешанный экспорт
Можно экспортировать и «главное», и дополнительные утилиты:

`utils.js`
```js
export default function log(msg) {
  console.log("LOG:", msg);
}

export const VERSION = "1.0.0";
export function warn(msg) {
  console.warn("WARNING:", msg);
}
```

`main.js`
```js
import log, { VERSION, warn } from './utils.js';

log("Test");          // LOG: Test
console.log(VERSION); // 1.0.0
warn("Be careful");   // WARNING: Be careful
```
