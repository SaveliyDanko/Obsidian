
[[call]]
[[apply]]
[[bind]]


---
JavaScript functions are defined with the `function` keyword.

###### **Function Declarations**
Functions are declared with the following syntax:
```js
function functionName(parameters) {  
  // _code to be executed_  
}
```

###### **Function Expressions**
A JavaScript function can also be defined using an expression.
A function expression can be stored in a variable:
```js
const x = function (a, b) {return a * b};
```
After a function expression has been stored in a variable, the variable can be used as a function:
```js
const x = function (a, b) {return a * b};  
let z = x(4, 3);
```
The function above is actually an anonymous function.

###### **Function() Constructor**
Functions can also be defined with a built-in JavaScript function constructor called `Function()`.
```js
const myFunction = new Function("a", "b", "return a * b");  
let x = myFunction(4, 3);
```

###### **Self-Invoking Functions**
Function expressions can be made "self-invoking".
A self-invoking expression is invoked (started) automatically, without being called.
Function expressions will execute automatically if the expression is followed by ().
You cannot self-invoke a function declaration.
You have to add parentheses around the function to indicate that it is a function expression:
```js
(function () {  
  let x = "Hello!!";  // I will invoke myself  
})();
```

###### **Functions are Objects**
The `typeof` operator in JavaScript returns "function" for functions.
But, JavaScript functions can best be described as objects.
JavaScript functions have both properties and methods.
The `arguments.length` property returns the number of arguments received when the function was invoked:
```js
function myFunction(a, b) {  
  return arguments.length;  
}
```
The `toString()` method returns the function as a string:
```js
function myFunction(a, b) {  
  return a * b;  
}  
let text = myFunction.toString();
```

###### **Arrow functions**
Arrow functions allows a shorter syntax for function expressions.
You don't need the function keyword, the return keyword, and the curly brackets:
```js
let myFunction = (a, b) => a * b;
```

###### **Arrow Functions Return Value by Default:**
If the function has only one statement that returns a value, you can remove the brackets and the `return` keyword:
```js
let hello = () => "Hello World!";
```

###### **Arrow Function With Parameters:**
```js
let hello = (val) => "Hello " + val;
```

###### **`this` in Arrow functions**
- В обычных функциях `function` значение `this` зависит от того, кто вызвал функцию.  
    Оно может быть:
    - `window` (если функция вызвана глобально в браузере)
    - DOM-элемент (если функция используется как обработчик события на элементе)
    - Любой другой объект, если вызов идёт как метод этого объекта
- В стрелочных функциях `() => {}` нет собственного `this`.  
    Вместо этого стрелочная функция наследует `this` из внешней (лексической) области — из того контекста, в котором она была создана.

###### **Hoisting in Arrow functions**
- Стрелочные функции не поднимаются (не hoisted)
    - Их нельзя вызывать до объявления.
    - Нужно всегда сначала объявить, потом использовать.

###### **Function Parameters and Arguments**
```js
function functionName(parameter1, parameter2, parameter3) {  
  // _code to be executed_  
}
```
Function parameters are the names listed in the function definition.
Function arguments are the real values passed to (and received by) the function.
- JavaScript function definitions do not specify data types for parameters.
- JavaScript functions do not perform type checking on the passed arguments.
- JavaScript functions do not check the number of arguments received.

###### **Default Parameters**
If a function is called with missing arguments (less than declared), the missing values are set to `undefined`.
ES6 allows function parameters to have default values.
```js
function myFunction(x, y = 10) {  
  return x + y;  
}  
myFunction(5);
```

###### **Rest Parameter**
The rest parameter (...) allows a function to treat an indefinite number of arguments as an array:
```js
function sum(...args) {  
  let sum = 0;  
  for (let arg of args) sum += arg;  
  return sum;  
}  
  
let x = sum(4, 9, 16, 25, 29, 100, 66, 77);
```

###### **Function as a Method**
In JavaScript you can define functions as object methods.
```js
const myObject = {  
  firstName:"John",  
  lastName: "Doe",  
  fullName: function () {  
    return this.firstName + " " + this.lastName;  
  }  
}  
myObject.fullName();         // Will return "John Doe"
```

###### **Сокращённая запись метода**
В JavaScript существует более короткая форма записи методов в объекте:
  ```javascript
user = {
	sayHi() {
		alert("Привет!");
	}
};
```
Эта запись эквивалентна следующей:
```javascript
user = {
	sayHi: function() {
		alert("Привет!");
	}
};
```
Сокращённый синтаксис предпочтителен для большей читаемости кода.

###### **this**
In JavaScript, the `this` keyword refers to an object.
The `this` keyword refers to different objects depending on how it is used:
- Alone, `this` refers to the global object.
- In a function, `this` refers to the global object.
- In a function, in strict mode, `this` is `undefined`.
- In an object method, `this` refers to the object.
- In an event, `this` refers to the element that received the event.
- Methods like `call()`, `apply()`, and `bind()` can refer `this` to any object.
