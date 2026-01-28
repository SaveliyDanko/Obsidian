###### **`@include` — подключение миксинов**
Позволяет вставлять код миксина в нужное место, как функцию в программировании. Используется вместе с `@mixin`.

###### **Пример:**
```scss
@mixin flex-center {
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  @include flex-center;
}
```

Можно передавать параметры:
```scss
@mixin size($width, $height) {
  width: $width;
  height: $height;
}

.box {
  @include size(100px, 200px);
}
```
