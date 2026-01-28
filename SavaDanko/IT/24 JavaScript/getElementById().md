`Document.getElementById(id)` — это метод объекта `document`, который возвращает первый элемент в DOM с указанным значением атрибута `id`.  
Если элемент не найден, возвращает `null`.

###### **Синтаксис**
```js
const element = document.getElementById(id);
```
- `id` — строка с точным значением атрибута `id`.
- Возвращает один элемент (`Element`) или `null`.
    
###### **Пример**
```html
<div id="app">Hello</div>

<script>
  const el = document.getElementById('app');
  console.log(el.textContent); // Hello
</script>
```

###### **Особенности**
1. Поиск по уникальному ID  
    Атрибут `id` должен быть уникальным в пределах документа.  
    Если есть несколько одинаковых `id` (что нарушает спецификацию), метод вернёт первый найденный.
    
2. Без `#` в аргументе  
    В отличие от `querySelector('#id')`, в `getElementById()` не нужно указывать `#`.
    
3. Доступ только в `document`  
    Это метод `document`, не `Element`.  
    То есть нельзя сделать:
    ```js
    someElement.getElementById('id');
    ```
    
    Работает только:
    ```js
    document.getElementById('id');
    ```
