###### **`@function` — пользовательская функция**
`@function` возвращает одно значение и используется для вычислений, преобразований и логики внутри SCSS.

###### **Пример**
```scss
@function rem($px) {
  @return $px / 16 * 1rem;
}
```

Преобразует пиксели в `rem`, если считать, что `1rem = 16px`.
```scss
.title {
  font-size: rem(24); // → 1.5rem
}
```

###### **Пример с логикой**
```scss
@function theme-color($name) {
  @if $name == 'primary' {
    @return #3498db;
  } @else if $name == 'danger' {
    @return #e74c3c;
  } @else {
    @return black;
  }
}

.alert {
  color: theme-color('danger'); // → #e74c3c
}
```
