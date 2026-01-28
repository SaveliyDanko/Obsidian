#css 

[font-family](https://cssreference.io/property/font-family/)

---
When using *multiple* values, the `font-family` list of *font families* defines the *priority* in which the browser should choose the font family.

The browser will look for each family on the user's *computer* and in any *@font-face* resource.

The list is prioritized from *left* to *right*: it will use the first value if it's available, or go to the next one, until the end of the list is reached. The *default* font family is defined by the browser preferences.

```css
font-family: "Source Sans Pro", "Arial", sans-serif;
```
