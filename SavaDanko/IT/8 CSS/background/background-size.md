#css 

[background-size](https://cssreference.io/property/background-size/)

---
Defines the size of the background image.

```css
background-size: auto auto;
```
The background image will retain its original size.
For example, this background image is `960px` by `640px` large. Its aspect ratio is 3 by 2. It's bigger than its container (which is `150px` high) and will thus be clipped.

You can specify a size in pixels:
- the first value is the horizontal size
- the second is the vertical size
```css
background-size: 120px 80px;
```

You can use percentage values as well. Beware that this can alter the aspect ratio of the background image, and lead to unexpected results.
```css
background-size: 100% 50%;
```

The keyword `contain` will resize the background image to make sure it remains fully visible.
```css
background-size: contain;
```

The keyword `cover` will resize the background image to make sure the element is fully covered.
```css
background-size: cover;
```