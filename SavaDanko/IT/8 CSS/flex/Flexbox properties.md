###### **display**
This defines a flex container; inline or block depending on the given value. It enables a flex context for all its direct children.
```css
.container {
  display: flex; /* or inline-flex */
}
```

###### **flex-direction**
This establishes the main-axis, thus defining the direction flex items are placed in the flex container.
![the four possible values of flex-direction being shown: top to bottom, bottom to top, right to left, and left to right](https://css-tricks.com/wp-content/uploads/2018/10/flex-direction.svg)
```css
.container {
  flex-direction: row | row-reverse | column | column-reverse;
}
```

###### **flex-wrap**
![two rows of boxes, the first wrapping down onto the second](https://css-tricks.com/wp-content/uploads/2018/10/flex-wrap.svg)
```css
.container {
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```
- `nowrap` (default): all flex items will be on one line
- `wrap`: flex items will wrap onto multiple lines, from top to bottom.
- `wrap-reverse`: flex items will wrap onto multiple lines from bottom to top.

###### **flex-flow**
This is a shorthand for the `flex-direction` and `flex-wrap` properties, which together define the flex container’s main and cross axes. The default value is `row nowrap`.
```css
.container {
  flex-flow: column wrap;
}
```

###### **justify-content**
![flex items within a flex container demonstrating the different spacing options](https://css-tricks.com/wp-content/uploads/2018/10/justify-content.svg)
```css
.container {
  justify-content: flex-start | flex-end | center | space-between | space-around | space-evenly;
}
```

###### **align-items**
![demonstration of differnet alignment options, like all boxes stuck to the top of a flex parent, the bottom, stretched out, or along a baseline](https://css-tricks.com/wp-content/uploads/2018/10/align-items.svg)
```css
.container {
  align-items: stretch | flex-start | flex-end | center | baseline;
}
```

###### **align-content**
![examples of the align-content property where a group of items cluster at the top or bottom, or stretch out to fill the space, or have spacing.](https://css-tricks.com/wp-content/uploads/2018/10/align-content.svg)
```css
.container {
  align-content: flex-start | flex-end | center | space-between | space-around;
}
```

###### **gap, row-gap, column-gap**
![](https://css-tricks.com/wp-content/uploads/2021/09/gap-1.svg)
The gap property explicitly controls the space between flex items. It applies that spacing only between items not on the outer edges.
```css
.container {
  display: flex;
  ...
  gap: 10px;
  gap: 10px 20px; /* row-gap column gap */
  row-gap: 10px;
  column-gap: 20px;
}
```


---
###### **order**
![Diagram showing flexbox order. A container with the items being 1 1 1 2 3, -1 1 2 5, and 2 2 99.](https://css-tricks.com/wp-content/uploads/2018/10/order.svg)
By default, flex items are laid out in the source order. However, the `order` property controls the order in which they appear in the flex container.
```css
.item {
  order: 5; /* default is 0 */
}
```

###### **flex-grow**
![two rows of items, the first has all equally-sized items with equal flex-grow numbers, the second with the center item at twice the width because its value is 2 instead of 1.](https://css-tricks.com/wp-content/uploads/2018/10/flex-grow.svg)
This defines the ability for a flex item to grow if necessary. It accepts a unitless value that serves as a proportion. It dictates what amount of the available space inside the flex container the item should take up.
```css
.item {
  flex-grow: 4; /* default 0 */
}
```

###### **flex-shrink**
This defines the ability for a flex item to shrink if necessary.
```css
.item {
  flex-shrink: 3; /* default 1 */
}
```

###### **flex-basis**
Это свойство определяет базовый размер элемента до того, как будет распределено оставшееся пространство в контейнере.  
Оно может принимать конкретное значение длины (например, `20%`, `5rem` и т.п.) или ключевое слово.
```css
.item {
  flex-basis:  | auto; /* default auto */
}
```

###### **align-self**
![One item with a align-self value is positioned along the bottom of a flex parent instead of the top where all the rest of the items are.](https://css-tricks.com/wp-content/uploads/2018/10/align-self.svg)
This allows the default alignment (or the one specified by `align-items`) to be overridden for individual flex items.
```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```