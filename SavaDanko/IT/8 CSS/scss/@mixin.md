###### **`@mixin` — миксин (вставка блока стилей)**
`@mixin` позволяет определить блок CSS-кода, который можно многократно вставлять с помощью `@include`.

###### Пример простого миксина
```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.box {
  @include flex-center;
}
```

В итоге `.box` будет:
```css
.box {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

###### **Миксин с параметрами**
```scss
@mixin size($width, $height) {
  width: $width;
  height: $height;
}

.card {
  @include size(200px, 300px);
}
```

Подставляется как шаблон:
```css
.card {
  width: 200px;
  height: 300px;
}
```