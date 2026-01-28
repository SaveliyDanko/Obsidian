`useState` — это хук (hook) в React, который позволяет добавить состояние (state) в функциональный компонент.

###### **Синтаксис**
```jsx
import { useState } from "react";

const [value, setValue] = useState(initialValue);
```
- `value` — текущее значение состояния.
- `setValue` — функция для изменения состояния.
- `initialValue` — начальное значение (число, строка, объект, массив и т.д.).

###### **Пример: счётчик**
```jsx
import { useState } from "react";

export default function Counter() {
  const [count, setCount] = useState(0); // начальное значение 0

  return (
    <div>
      <p>Счётчик: {count}</p>
      <button onClick={() => setCount(count + 1)}>+1</button>
      <button onClick={() => setCount(count - 1)}>-1</button>
    </div>
  );
}
```
При нажатии на кнопку вызывается `setCount`, React перерисовывает компонент с новым значением.

###### **Обновление на основе предыдущего значения**
Если новое значение зависит от старого, лучше передавать функцию в setValue:
```jsx
setCount(prev => prev + 1);
```
Это защищает от устаревших значений в асинхронных обновлениях.