###### **`@content` — вставка пользовательского содержимого в миксин**
Позволяет вставить произвольный блок стилей внутрь миксина. Используется, когда ты хочешь передавать "контент" в миксин, как слот в компонентах.

###### **Пример:**
```scss
@mixin card {
  border: 1px solid #ccc;
  padding: 1rem;
  border-radius: 8px;

  @content; // сюда подставится переданный блок
}

.product {
  @include card {
    background-color: #f9f9f9;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
  }
}
```

Результат:
```css
.product {
  border: 1px solid #ccc;
  padding: 1rem;
  border-radius: 8px;
  background-color: #f9f9f9;
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.1);
}
```
