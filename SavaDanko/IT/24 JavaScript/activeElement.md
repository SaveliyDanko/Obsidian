`document.activeElement` — это свойство объекта `document`, которое возвращает элемент в DOM, на котором сейчас находится фокус.  
Если ни один элемент не в фокусе, возвращает `body` (или `null` в некоторых сценариях).

###### **Синтаксис**
```js
const el = document.activeElement;
```
- Возвращает объект `Element`.
- Если фокус не установлен — чаще всего вернёт `document.body`.

###### **Пример**
```html
<input type="text" id="name" placeholder="Введите имя">

<script>
  document.getElementById('name').addEventListener('focus', () => {
    console.log(document.activeElement); // <input id="name">
  });
</script>
```

###### **Когда меняется `activeElement`**
- Когда пользователь кликает по элементу, который может получать фокус (`input`, `textarea`, `button`, ссылка с `href`, элемент с `tabindex`).
- Когда фокус меняется через JS:
    ```js
    element.focus();
    ```
- При навигации с клавиатуры (Tab, Shift+Tab).