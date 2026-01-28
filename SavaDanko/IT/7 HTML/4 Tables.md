HTML-таблицы используются для отображения табличных данных.
```html
<table>
	<caption>Заголовок</caption>
	<thead>
		<tr>
			<th>head 1</th>
			<th>head 2</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td>body 1</td>
			<td>body 2</td>
		</tr>
	</tbody>
</table>
```

- `table` - определяет таблицу
- `tr` - строка таблицы (table row)
- `th` - ячейка заголовка таблицы (table head)
- `td` - ячейка таблицы (table data)

- `caption` - название таблицы
- `thead`
- `tbody`
- `tfoot`

Группировка элементов
- `colspan` - объединяет ячейки по горизонтали
- `rowspan` - объединяет ячейки по вертикали
```html
<table>
	<tr>
		<th>Заголовок 1</th>
		<th>Заголовок 2</th>
		<th>Заголовок 3</th>
	</tr>
	<tr>
		<td colspan="2">Объединённая ячейка</td>
		<td>Данные 3</td>
	</tr>
</table>
```