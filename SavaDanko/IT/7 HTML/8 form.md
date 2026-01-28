Базовая HTML-форма создаётся с помощью тега `<form>`, внутри которого размещаются различные элементы формы, такие как `<input>`, `<button>`, `<select>` и другие.
```html
<form action="/submit" method="post">
	<label for="username">Имя пользователя:</label>
	<input type="text" id="username" name="username" required>
	
	<label for="password">Пароль:</label>
	<input type="password" id="password" name="password" required>
	
	<button type="submit">Отправить</button>
</form>
```

- `action` — указывает URL, на который будут отправлены данные формы
- `method` — указывает HTTP-метод, используемый при отправке формы. Основные значения:
	- `get`: добавляет данные формы в адресную строку.
	- `post`: отправляет данные в теле запроса.
- `target` - указывает, где отображать результат после отправки формы. Основные значения:
	- `_self`: (по умолчанию) — в текущем окне/вкладке.
	- `_blank`: в новой вкладке или окне.
	- `_parent`: в родительском фрейме.
	- `_top`: во всём окне браузера.


