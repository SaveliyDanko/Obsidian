Тег `<label>` в HTML используется для создания подписей к элементам формы `<input>`.

С помощью атрибута `for`
```html
<label for="username">Имя пользователя:</label>
<input type="text" id="username" name="username">
```

Обёртывание элемента `<input>` внутрь `<label>`
```html
<label>Имя пользователя:
  <input type="text" name="username">
</label>
```