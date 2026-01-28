**SCSS (Sassy CSS)** — синтаксис препроцессора Sass (Syntactically Awesome Stylesheets), который расширяет стандартные возможности CSS. 

SCSS — это надстройка над CSS, добавляющая мощные функции программирования: переменные, вложенность, функции, условия, миксины, импорт и наследование.

###### **Пример SCSS-кода**
```scss
$primary-color: #3498db;

	body {
		font-family: Arial, sans-serif;
		background-color: $primary-color;

		h1 {
			color: darken($primary-color, 10%);
		}

		.btn {
		    padding: 10px 20px;
		    background: $primary-color;
		    &:hover {
		      background: lighten($primary-color, 10%);
		      }
		}
}
```

###### **Пример использования миксина**
```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  @include flex-center;
  height: 100vh;
}
```
