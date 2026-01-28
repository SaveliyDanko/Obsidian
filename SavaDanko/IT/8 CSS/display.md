Sets the display behavior of the element.

###### **none**
```css
display: none;
```
The element is completely removed, as if it wasn't in the HTML code in the first place.

###### **inline**
```css
display: inline;
```
The element is turned into an inline element: it behaves like simple text.
Any `height` and `width` applied will have no effect.

###### **block**
```css
display: block;
```
The element is turned into a block element: it starts on a new line, and takes up the whole width.

###### **inline-block**
```css
display: inline-block;
```
The element shares properties of both an inline and a block element:
- inline because the element behaves like simple text, and inserts itself in a block of text
- Block because you can apply `height` and `width` values

###### **list-item**
```css
display: list-item;
```
The element behaves like a list item: `<li>`. The only difference with block is that a list item has a bullet point.

###### **table**
```css
display: table;
```
The element behaves like a table: `<table>`.
Its content and child elements behave like table cells.

###### **table-cell**
The element behaves like a table cell: `<td>` or `<th>`.
Its content and child elements behave like table cells.

###### **table-row**
```css
display: table-row;
```
The element behaves like a table row: `<tr>`.
Its content and child elements behave like table cells.

###### **flex**
```css
display: flex;
```
The element is turned into an flexbox container. On its own, it behaves like a block element.
Its child elements will be turned into flexbox items.

###### **inline-flex**
```css
display: inline-flex;
```
The element shares properties of both an inline and a flexbox element:
- inline because the element behaves like simple text, and inserts itself in a block of text
- flexbox because its child element will be turned into flexbox item

###### **grid**
```css
display: grid;
```
The element is turned into an grid container. On its own, it behaves like a block element.
Its child elements will be turned into grid items.

###### **inline-grid**
```css
display: inline-grid;
```
The element shares properties of both an inline and a grid element:
- inline because the element behaves like simple text, and inserts itself in a block of text
- grid because its child element will be turned into flexbox items

