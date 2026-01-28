#css 

---
###### **display**
Defines the element as a grid container and establishes a new grid formatting context for its contents.
- `grid` – generates a block-level grid
- `inline-grid` – generates an inline-level grid

```css
.container {
		display: grid | inline-grid;
}
```

###### **grid-template-rows / grid-template-columns**  
Defines the columns and rows of the grid with a space-separated list of values. The values represent the track size, and the space between them represents the grid line.
```css
.container {
		grid-template-columns: ...  ...;
		/* e.g. 
	    1fr 1fr
	    minmax(10px, 1fr) 3fr
	    repeat(5, 1fr)
	    50px auto 100px 1fr
		*/
		
		grid-template-rows: ... ...;
		/* e.g. 
	    min-content 1fr min-content
		100px 1fr max-content
		*/
}
```

Grid lines are automatically assigned positive numbers from these assignments (-1 being an alternate for the very last row).
![](https://css-tricks.com/wp-content/uploads/2018/11/template-columns-rows-01.svg)

But you can choose to explicitly name the lines. Note the bracket syntax for the line names:
```css
.container {
		grid-template-columns: [first] 40px [line2] 50px [line3] auto [col4-start] 50px [five] 40px [end];
		grid-template-rows: [row1-start] 25% [row1-end] 100px [third-line] auto [last-line];
}
```
![Grid with user named lines](https://css-tricks.com/wp-content/uploads/2018/11/template-column-rows-02.svg)

Note that a line can have more than one name. For example, here the second line will have two names: row1-end and row2-start:
```css
.container {
		grid-template-rows: [row1-start] 25% [row1-end row2-start] 25% [row2-end];
}
```

###### **grid-template**
A shorthand for setting `grid-template-rows`, `grid-template-columns`, and `grid-template-areas` in a single declaration.
```css
.container {
		grid-template:
		[row1-start] "header header header" 25px [row1-end]
		[row2-start] "footer footer footer" 25px [row2-end]
		/ auto 50px auto;
}
```

That’s equivalent to this:
```css
.container {
		grid-template-rows: [row1-start] 25px [row1-end row2-start] 25px [row2-end];
		grid-template-columns: auto 50px auto;
		grid-template-areas: 
		"header header header" 
		"footer footer footer";
}
```
###### **grid-template-areas**
Defines a grid template by referencing the names of the grid areas which are specified with the grid-area property. Repeating the name of a grid area causes the content to span those cells. A period signifies an empty cell. The syntax itself provides a visualization of the structure of the grid.
###### **grid-area**
```css
.item {
		grid-area: <name> | <row-start> / <column-start> / <row-end> / <column-end>;
}
```

###### **grid-template-areas**
Defines a grid template by referencing the names of the grid areas which are specified with the `grid-area` property. Repeating the name of a grid area causes the content to span those cells. A period signifies an empty cell. The syntax itself provides a visualization of the structure of the grid.
```css
.container {
		grid-template-areas:
		"<grid-area-name> | . | none | ..."
		"...";
}
```

```css
.item-a {
		grid-area: header;
}

.item-b {
		grid-area: main;
}

.item-c {
		grid-area: sidebar;
}

.item-d {
		grid-area: footer;
}

.container {
		display: grid;
		grid-template-columns: 50px 50px 50px 50px;
		grid-template-rows: auto;
		grid-template-areas: 
	    "header header header header"
	    "main main . sidebar"
	    "footer footer footer footer";
}
```
That’ll create a grid that’s four columns wide by three rows tall. The entire top row will be composed of the header area. The middle row will be composed of two main areas, one empty cell, and one sidebar area. The last row is all footer.
![Example of grid-template-areas](https://css-tricks.com/wp-content/uploads/2018/11/dddgrid-template-areas.svg)
Each row in your declaration needs to have the same number of cells.

###### **column-gap / row-gap**
Specifies the size of the grid lines. You can think of it like setting the width of the gutters between the columns/rows.
```css
.container {
		/* standard */
		column-gap: <line-size>;
		row-gap: <line-size>;
}
```
![Example of grid-column-gap and grid-row-gap](https://css-tricks.com/wp-content/uploads/2018/11/dddgrid-gap.svg)

###### **gap**
A shorthand for `row-gap` and `column-gap`.
```css
.container {
		/* standard */
		gap: <grid-row-gap> <grid-column-gap>;
}
```

###### **justify-items**
Aligns grid items along the inline (row) axis.
```css
.container {
		justify-items: start | end | center | stretch;
}
```
- `start` – aligns items to be flush with the start edge of their cell
![Example of justify-items set to start](https://css-tricks.com/wp-content/uploads/2018/11/justify-items-start.svg)
- `end` – aligns items to be flush with the end edge of their cell
![Example of justify-items set to end](https://css-tricks.com/wp-content/uploads/2018/11/justify-items-end.svg)
- `center` – aligns items in the center of their cell
![Example of justify-items set to center](https://css-tricks.com/wp-content/uploads/2018/11/justify-items-center.svg)
- `stretch` – fills the whole width of the cell (this is the default)
![Example of justify-items set to stretch](https://css-tricks.com/wp-content/uploads/2018/11/justify-items-stretch.svg)
###### **align-items**
Aligns grid items along the block (column) axis
```css
.container {
		align-items: start | end | center | stretch;
}
```
- `start` – aligns items to be flush with the start edge of their cell
![Example of align-items set to start](https://css-tricks.com/wp-content/uploads/2018/11/align-items-start.svg)
- `end` – aligns items to be flush with the end edge of their cell
![Example of align-items set to end](https://css-tricks.com/wp-content/uploads/2018/11/align-items-end.svg)
- `center` – aligns items in the center of their cell
![Example of align-items set to center](https://css-tricks.com/wp-content/uploads/2018/11/align-items-center.svg)
- `stretch` – fills the whole height of the cell (this is the default)
![Example of align-items set to stretch](https://css-tricks.com/wp-content/uploads/2018/11/align-items-stretch.svg)
###### **place-items**
`place-items` sets both the `align-items` and `justify-items` properties in a single declaration.
```css
.center {
		display: grid;
		place-items: center / end;
}
```

###### **justify-content**
Sometimes the total size of your grid might be less than the size of its grid container. This could happen if all of your grid items are sized with non-flexible units like `px`. In this case you can set the alignment of the grid within the grid container.
```css
.container {
	justify-content: start | end | center | stretch | space-around | space-between;  
}
```

- `start` – aligns the grid to be flush with the start edge of the grid container
![Example of justify-content set to start](https://css-tricks.com/wp-content/uploads/2018/11/justify-content-start.svg)
- `end` – aligns the grid to be flush with the end edge of the grid container
![Example of justify-content set to end](https://css-tricks.com/wp-content/uploads/2018/11/justify-content-end.svg)
- `center` – aligns the grid in the center of the grid container
![Example of justify-content set to center](https://css-tricks.com/wp-content/uploads/2018/11/justify-content-center.svg)
- `stretch` – resizes the grid items to allow the grid to fill the full width of the grid container
![Example of justify-content set to stretch](https://css-tricks.com/wp-content/uploads/2018/11/justify-content-stretch.svg)
- `space-around` – places an even amount of space between each grid item, with half-sized spaces on the far ends
![Example of justify-content set to space-around](https://css-tricks.com/wp-content/uploads/2018/11/justify-content-space-around.svg)
- `space-between` – places an even amount of space between each grid item, with no space at the far ends
![Example of justify-content set to space-between](https://css-tricks.com/wp-content/uploads/2018/11/justify-content-space-between.svg)
- `space-evenly` – places an even amount of space between each grid item, including the far ends
![Example of justify-content set to space-evenly](https://css-tricks.com/wp-content/uploads/2018/11/justify-content-space-evenly.svg)
###### **align-content**
- `start` – aligns the grid to be flush with the start edge of the grid container
![Example of align-content set to start](https://css-tricks.com/wp-content/uploads/2018/11/align-content-start.svg)
- `end` – aligns the grid to be flush with the end edge of the grid container
![Example of align-content set to end](https://css-tricks.com/wp-content/uploads/2018/11/align-content-end.svg)
- `center` – aligns the grid in the center of the grid container
![Example of align-content set to center](https://css-tricks.com/wp-content/uploads/2018/11/align-content-center.svg)
- `stretch` – resizes the grid items to allow the grid to fill the full height of the grid container
![Example of align-content set to stretch](https://css-tricks.com/wp-content/uploads/2018/11/align-content-stretch.svg)
- `space-around` – places an even amount of space between each grid item, with half-sized spaces on the far ends
![Example of align-content set to space-around](https://css-tricks.com/wp-content/uploads/2018/11/align-content-space-around.svg)
- `space-between` – places an even amount of space between each grid item, with no space at the far ends
![Example of align-content set to space-between](https://css-tricks.com/wp-content/uploads/2018/11/align-content-space-between.svg)
- `space-evenly` – places an even amount of space between each grid item, including the far ends
![Example of align-content set to space-evenly](https://css-tricks.com/wp-content/uploads/2018/11/align-content-space-evenly.svg)

###### **place-content**
`place-content` sets both the `align-content` and `justify-content` properties in a single declaration.
```css
.center {
		display: grid;
		place-content: center / space-between;
}
```

###### **justify-self**
Aligns a grid item inside a cell along the inline (row) axis.
This value applies to a grid item inside a single cell.
```css
.item {
		justify-self: start | end | center | stretch;
}
```

- `start` – aligns the grid item to be flush with the start edge of the cell
![Example of justify-self set to start](https://css-tricks.com/wp-content/uploads/2018/11/justify-self-start.svg)
- `end` – aligns the grid item to be flush with the end edge of the cell
![alt="Example](https://css-tricks.com/wp-content/uploads/2018/11/justify-self-end.svg)
- `center` – aligns the grid item in the center of the cell
![Example of justify-self set to center](https://css-tricks.com/wp-content/uploads/2018/11/justify-self-center.svg)
- `stretch` – fills the whole width of the cell (this is the default)
![Example of justify-self set to stretch](https://css-tricks.com/wp-content/uploads/2018/11/justify-self-stretch.svg)

###### **align-self**
Aligns a grid item inside a cell along the block (column) axis.
```css
.item {
		align-self: start | end | center | stretch;
}
```

- `start` – aligns the grid item to be flush with the start edge of the cell
![Example of align-self set to start](https://css-tricks.com/wp-content/uploads/2018/11/align-self-start.svg)
- `end` – aligns the grid item to be flush with the end edge of the cell
![Example of align-self set to end](https://css-tricks.com/wp-content/uploads/2018/11/align-self-end.svg)
- `center` – aligns the grid item in the center of the cell
![Example of align-self set to center](https://css-tricks.com/wp-content/uploads/2018/11/align-self-center.svg)
- `stretch` – fills the whole height of the cell (this is the default)
![Example of align-self set to stretch](https://css-tricks.com/wp-content/uploads/2018/11/align-self-stretch.svg)

###### **place-self**
`place-self` sets both the `align-self` and `justify-self` properties in a single declaration.
```css
.item-a {
		place-self: center stretch;
}
```

