###### **`@forward` — переэкспорт модулей**
- Используется внутри промежуточных модулей (например, index-файлов)
- Позволяет перенаправить содержимое SCSS-файла дальше
- Часто используется в библиотеках или крупных проектах
    
###### **Пример:**
```scss
// _colors.scss
$primary: #3498db;
```

```scss
// _index.scss
@forward 'colors';
```

```scss
// style.scss
@use 'index';

.button {
  background-color: index.$primary;
}
```

###### **Типичная структура SCSS с `@use` и `@forward`**
```
/styles
  /utils
    _variables.scss
    _mixins.scss
    _functions.scss
    _index.scss
  main.scss
```
