Тег `<input>` используется в HTML для создания различных полей ввода.
```html
<input type="text" name="username" id="username">
```

#### Типы полей ввода
1. **Текстовое поле (`type="text"`)**
```html
<input type="text" name="username" placeholder="Введите имя пользователя">
```

2. **Пароль (`type="password"`)**
```html
<input type="password" name="password" placeholder="Введите пароль">
```

3. **Email (`type="email"`)**
```html
<input type="email" name="email" placeholder="Введите email">
```

4. **Число (`type="number"`)**
```html
<input type="number" name="quantity" min="1" max="10">
```

5. **Дата (`type="date"`)**
```html
<input type="date" name="birthday">
```

6. **Флажок (`type="checkbox"`)**
```html
<input type="checkbox" name="subscribe" value="newsletter">
```

7. **Переключатели (`type="radio"`)**
```html
<input type="radio" name="gender" value="male"> Мужской
<input type="radio" name="gender" value="female"> Женский
```

8. **Загрузка файла (`type="file"`)**
```html
<input type="file" name="profile_picture">
```

9. **Кнопка отправки (`type="submit"`)**
```html
<input type="submit" value="Отправить">
```

10. **Кнопка сброса (`type="reset"`)**
```html
<input type="reset" value="Сбросить">
```

11. **Выбор цвета (`type="color"`)**
```html
<input type="color" name="favcolor">
```

12. **Диапазон (`type="range"`)**
```html
<input type="range" name="points" min="0" max="100">
```
