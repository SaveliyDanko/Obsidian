`addEventListener()` — это метод, который позволяет навесить обработчик события на элемент (или объект, который поддерживает события), при этом:
- можно добавить несколько обработчиков одного события,
- можно управлять порядком и фазой срабатывания,
- можно легко удалить обработчик при необходимости.


###### **Синтаксис**
```js
target.addEventListener(type, listener [, options]);
```
- `target` — объект, который поддерживает события (`Element`, `Document`, `Window`, `XMLHttpRequest` и т.д.).
- `type` — строка с названием события (`'click'`, `'input'`, `'keydown'`... без `on`).
- `listener` — функция-обработчик (или объект с методом `handleEvent`).
- `options` _(необязательный)_ — объект или булево значение:
    - `{ capture: false, once: false, passive: false }`
    - Если указать просто `true`/`false`, это будет значением `capture`.
        

###### **Пример**
```js
document.getElementById('btn').addEventListener('click', () => {
  console.log('Кнопка нажата');
});
```

###### **Опции подробно**
`capture`
- По умолчанию: `false` — событие ловится **на фазе всплытия**.
- Если `true` — обработчик сработает на **фазе погружения**.
```js
element.addEventListener('click', handler, { capture: true });
```

`once`
- Если `true` — обработчик сработает только один раз, после чего будет удалён автоматически.
```js
btn.addEventListener('click', handler, { once: true });
```

`passive`
- Если `true` — обработчик гарантированно не будет вызывать `preventDefault()`.
- Используется для оптимизации, например, на событиях `scroll` или `touchmove`.
```js
window.addEventListener('scroll', handler, { passive: true });
```

###### **Удаление обработчика**
Чтобы удалить обработчик, нужно передать **ту же самую** функцию и такие же параметры:
```js
function onClick() {
  console.log('Клик!');
}

btn.addEventListener('click', onClick);
btn.removeEventListener('click', onClick);
```
Если использовать анонимную функцию в `addEventListener`, удалить её потом будет невозможно.

###### **Несколько обработчиков**
В отличие от `element.onclick = handler`, `addEventListener()` позволяет добавлять несколько обработчиков одного события:
```js
btn.addEventListener('click', () => console.log('Первый'));
btn.addEventListener('click', () => console.log('Второй'));
```

###### **Объект вместо функции**
Можно передать объект с методом `handleEvent`:
```js
const handlerObj = {
  handleEvent(event) {
    console.log('Событие:', event.type);
  }
};
btn.addEventListener('click', handlerObj);
```
