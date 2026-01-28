- **`focusin`** — срабатывает, когда элемент получает фокус, и всплывает (в отличие от `focus`).
- **`focusout`** — срабатывает, когда элемент теряет фокус, и всплывает (в отличие от `blur`).
Это значит, что можно отлавливать фокус и его потерю на родительском элементе, используя делегирование событий.

###### **Синтаксис**
```js
element.addEventListener('focusin', handler);
element.addEventListener('focusout', handler);
```
- Работает и на `document`, и на конкретных контейнерах.
    
###### **Пример — отлавливаем фокус во всей форме**
```html
<form id="myForm">
  <input type="text" placeholder="Имя">
  <input type="email" placeholder="Email">
</form>

<script>
const form = document.getElementById('myForm');

form.addEventListener('focusin', e => {
  console.log('Фокус перешёл на', e.target);
  e.target.style.backgroundColor = '#e0f7fa';
});

form.addEventListener('focusout', e => {
  console.log('Фокус ушёл с', e.target);
  e.target.style.backgroundColor = '';
});
</script>
```
Здесь обработчик висит один раз на форме, а не на каждом поле.