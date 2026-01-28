`querySelector()` — это метод `Document` и `Element`, который возвращает первый элемент, соответствующий переданному CSS-селектору.  
Если элемент не найден, возвращает `null`.

###### **Синтаксис**
```js
const element = parent.querySelector(selectors);
```
- `parent` — `document` или любой DOM-элемент, внутри которого искать.
- `selectors` — строка с CSS-селектором (можно комбинировать теги, классы, id, псевдоклассы).
    

###### **Примеры**
По ID
```js
document.querySelector('#app');
```

По классу
```js
document.querySelector('.btn-primary');
```

По тегу
```js
document.querySelector('header');
```

Комбинированный селектор
```js
document.querySelector('ul.menu > li.active a');
```

От конкретного элемента
```js
const menu = document.getElementById('menu');
menu.querySelector('li:first-child');
```

###### **Возвращаемое значение**
- Первый найденный элемент в порядке обхода DOM.
- `null`, если совпадений нет.