Тег `<button>` используется для создания кликабельных кнопок на веб-странице.

```html
<button>Нажми меня</button>
```

#### Существует три основных типа:

Кнопка отправки (`type="submit"`)
```html
<form action="/submit" method="post">
	<button type="submit">Отправить</button>
</form>
```

Кнопка сброса (`type="reset"`)
```html 
<form>
	<input type="text" name="username" value="JohnDoe">
	<button type="reset">Сбросить</button>
</form>
```

Обычная кнопка (`type="button"`)
```html
<button type="button" onclick="alert('Кнопка нажата!')">Нажми меня</button>
```

`value` - значение, которое будет отправлено на сервер при отправке формы
`name` — имя кнопки, может использоваться при отправке формы