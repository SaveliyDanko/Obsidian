```js
lel year = prompt('In what year was the first EMACS specification created?');
if (year = 2015) {
	alert('You are right');
} else if (year > 2015){
	alert('You year is later');
} else {
	alert('You are wrong');
}
```

Мы также можем передать заранее вычисленное в переменной логическое значение в `if`, например так:
```js
let condition = (year == 2015);

if (condition) {
// ...
}
```

---
#### Тернарный оператор 
```js
let result = condition ? value1 : value2
```
Сначала вычисляется `условие`: если оно истинно, тогда возвращается `значение1`, в противном случае – `значение2`.

Последовательность операторов вопросительного знака `?` позволяет вернуть значение, которое зависит от более чем одного условия.
```js
let age = prompt('Возраст', 18);

let message = (age < 3) ? "Hello Baby" : 
		(age < 18) ? "Hello" : 
		(age < 100) ? "Good Morning" : 
		"Your age is incredible"; 

alert(message);
```