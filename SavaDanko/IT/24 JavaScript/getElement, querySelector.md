#js 

---
###### **`getElementById`**
Если у элемента есть атрибут `id`, то мы можем получить его вызовом `document.getElementById(id)`, где бы он ни находился:
```js
let elem = document.getElementById('elem');
```
Значение `id` должно быть уникальным. В документе может быть только один элемент с данным `id`.

###### **`querySelectorAll`**
`elem.querySelectorAll(css)` $-$ возвращает все элементы внутри `elem`, удовлетворяющие данному CSS-селектору.

###### **`querySelector`**
`elem.querySelector(css)` $-$ возвращает первый элемент, соответствующий данному CSS-селектору.

###### **`matches`**
elem.matches(css) $-$ проверяет, удовлетворяет ли elem CSS-селектору, и возвращает true или false.

###### **`closest`**
`elem.closest(css)` $-$ ищет ближайшего предка, который соответствует CSS-селектору. Сам элемент также включается в поиск.