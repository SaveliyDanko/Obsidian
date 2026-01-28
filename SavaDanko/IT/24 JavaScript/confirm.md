Синтаксис:
```js
rusult = confirm(question);
```

Функция `confirm` отображает модальное окно с текстом вопроса `question` и двумя кнопками: OK и Отмена.
Результат – `true`, если нажата кнопка OK. В других случаях – `false`.

Например:
```js
let isBoss = confirm("Ты здесь главный?");
alert(isBoss); // true, если нажать "OK"
```

