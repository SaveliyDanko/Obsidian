###### **Что значит «чистый» в программировании?**
Термин пришёл из функционального программирования.  
Чистая функция — это функция, которая:
1. Возвращает один и тот же результат при одинаковых входных данных.
2. Не имеет побочных эффектов (не меняет внешние переменные, не работает с сетью/DOM напрямую и т. п.).

Пример чистой функции:
```js
function add(a, b) {
  return a + b; // всегда возвращает одно и то же при одних входных данных
}
```

Нечистая:
```js
let counter = 0;
function addAndLog(a, b) {
  counter++;
  console.log(a + b);
  return a + b;
}
```
Здесь побочный эффект — изменение `counter` и `console.log`.

###### **Чистый компонент в React**
В React чистый компонент — это компонент, который:
- Рендерит одинаковый UI при одинаковых `props` и `state`.
- Не зависит от внешних изменений (например, случайных значений или глобальных переменных).
- Не вызывает ненужный ререндер.
    

###### **`React.PureComponent`**
В классах есть встроенный `React.PureComponent`, который автоматически делает поверхностное сравнение (`shallow compare`) `props` и `state`.
```jsx
import React, { PureComponent } from "react";

class MyComponent extends PureComponent {
  render() {
    console.log("Рендер!");
    return <div>{this.props.value}</div>;
  }
}

// Использование
<MyComponent value="Привет" />
```
Если `value` не изменится, React не будет повторно рендерить компонент.

Обычный `Component` всегда вызывает `render()`, даже если `props` не изменились.

###### **Чистые компоненты с `React.memo` (для функций)**
Для функциональных компонентов используют `React.memo` — это аналог `PureComponent`.
```jsx
import React from "react";

const MyComponent = React.memo(function MyComponent({ value }) {
  console.log("Рендер!");
  return <div>{value}</div>;
});

// Использование
<MyComponent value="Привет" />
```
Если `value` останется тем же самым, компонент не будет перерендерен.