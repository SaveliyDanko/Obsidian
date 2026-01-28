Тег `<select>` используется для создания выпадающего списка.

Элемент `<select>` содержит несколько элементов `<option>`, каждый из которых представляет отдельный пункт в списке:
```html
<select name="cars">
	<option value="volvo">Volvo</option>
	<option value="saab">Saab</option>
	<option value="mercedes">Mercedes</option>
	<option value="audi">Audi</option>
</select>
```

`multiple` - позволяет выбрать несколько вариантов:
```html
<select name="cars" multiple>
```

Тег `<optgroup>` используется для логической группировки связанных пунктов, особенно полезен при большом количестве опций:
```html
<select name="cars">
	<optgroup label="Шведские авто">
		<option value="volvo">Volvo</option>
		<option value="saab">Saab</option>
	</optgroup>

	<optgroup label="Немецкие авто">
		<option value="mercedes">Mercedes</option>
		<option value="audi">Audi</option>
	</optgroup>
</select>
```