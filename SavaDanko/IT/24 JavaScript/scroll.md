Событие **`scroll`** срабатывает каждый раз, когда пользователь прокручивает содержимое элемента или окна (`window`), а его позиция прокрутки (`scrollTop` / `scrollLeft`) изменяется.

###### **Где срабатывает**
- На `window` — при прокрутке страницы:
    ```js
    window.addEventListener('scroll', handler);
    ```
    
- На прокручиваемом элементе (например, `div` с `overflow: auto`):
    ```js
    const box = document.getElementById('box');
    box.addEventListener('scroll', handler);
    ```
    
###### **Пример**
```html
<div id="box" style="width:200px; height:100px; overflow:auto; border:1px solid;">
  <div style="height:300px; background:linear-gradient(white, gray);"></div>
</div>

<script>
const box = document.getElementById('box');
box.addEventListener('scroll', () => {
  console.log('Прокрутка! scrollTop =', box.scrollTop);
});
</script>
```

###### **Свойства, которые полезны при `scroll`**
- `element.scrollTop` — сколько пикселей прокручено сверху.
- `element.scrollLeft` — сколько пикселей прокручено слева.
- `window.scrollY` / `window.scrollX` — прокрутка окна.
- `element.scrollHeight` — полная высота содержимого.
- `element.clientHeight` — видимая высота элемента.
