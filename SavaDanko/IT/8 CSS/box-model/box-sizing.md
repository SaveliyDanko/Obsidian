#css 

[box-sizing](https://cssreference.io/property/box-sizing/)

---
Defines how the width and height of the element are calculated: whether they include the _padding_ and _borders_ or not.

---
```css
box-sizing: content-box;
```
The *width* and *height* of the element only apply to the *content* of the element.
For example, this element has
- `border-width: 12px`
- `padding: 30px`
- `width: 200px`
The full width is `24px` + `60px` + `200px` = `284px`.
The content has the defined width. The box accomodates for those dimensions.
![[Pasted image 20250531233029.png]]

---
```css
box-sizing: border-box;
```
The *width* and *height* of the element apply to all parts of the element: the *content*, the *padding* and the *borders*.
For example, this element has
- `border-width: 12px`
- `padding: 30px`
- `width: 200px`
The full width is `200px`, no matter what.
The box has the defined width. The content accomodates for those dimensions, and ends up being `200px` - `60px` - `24px` = `116px`.
![[Pasted image 20250531233109.png]]
