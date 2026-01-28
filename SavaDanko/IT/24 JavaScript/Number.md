#js 

---
[Number](https://learn.javascript.ru/number)

---
#### Способы записи числа
```javascript
let billion = 1000000000;
let billion = 1_000_000_000
```

В JavaScript, чтобы укоротить запись числа, мы можем добавить к нему букву `"e"` и указать необходимое количество нулей:
```javascript
let billion = 1e9;  // 1 миллиард, буквально: 1 и 9 нулей
alert( 7.3e9 );  // 7.3 миллиарда (7,300,000,000)

let mcs = 0.000001;
let ms = 1e-6; // шесть нулей слева от 1
```

#### Шестнадцатеричные, двоичные и восьмеричные числа
`hex`:
```javascript
alert( 0xff ); // 255
alert( 0xFF ); // 255 (то же самое, регистр не имеет значения)
```

`oct`:
```javascript
let b = 0o377; // восьмеричная форма записи числа 255
```

`bin`:
```js
let a = 0b11111111; // двоичная (бинарная) форма записи числа 255
```


#### `toString(base)`
Метод `num.toString(base)` возвращает строковое представление числа `num` в системе счисления `base`.
```javascript
let num = 255;

alert( num.toString(16) );  // ff
alert( num.toString(2) );   // 11111111
```

#### Округление
`Math.floor`
Округление в меньшую сторону: 3.1 -> 3, а -1.1 -> -2

`Math.ceil`
Округление в большую сторону: 3.1 -> 4, а -1.1 -> -1

`Math.round`
Округление до ближайшего целого: 3.1 -> 3, 3.6 -> 4, а -1.1 -> -1

`Math.trunc` (не поддерживается в Internet Explorer)
Производит удаление дробной части без округления: 3.1 -> 3, а -1.1 -> -1


Метод `toFixed(n)` округляет число до `n` знаков после запятой и возвращает строковое представление результата.
```javascript
let num = 12.34;
alert( num.toFixed(1) ); // "12.3"
```

#### Проверка: `isFinite` и `isNaN`
`isNaN(value)` преобразует значение в число и проверяет является ли оно `NaN`:
```javascript
alert( isNaN(NaN) ); // true
alert( isNaN("str") ); // true
alert( NaN === NaN ); // false
```

`isFinite(value)` преобразует аргумент в число и возвращает `true`, если оно является обычным числом, т.е. не `NaN/Infinity/-Infinity`:
```javascript
alert( isFinite("15") ); // true
alert( isFinite("str") ); // false, потому что специальное значение: NaN
alert( isFinite(Infinity) ); // false, потому что специальное значение: Infinity
```

#### `parseInt` и `parseFloat`
Читают число из строки:
```javascript
alert( parseInt('100px') ); // 100
alert( parseFloat('12.5em') ); // 12.5

alert( parseInt('12.3') ); // 12, вернётся только целая часть
alert( parseFloat('12.3.4') ); // 12.3, произойдёт остановка чтения на второй точке
```
Функции `parseInt/parseFloat` вернут `NaN`, если не смогли прочитать ни одну цифру:
```javascript
alert( parseInt('a123') ); // NaN, на первом символе происходит остановка чтения
```