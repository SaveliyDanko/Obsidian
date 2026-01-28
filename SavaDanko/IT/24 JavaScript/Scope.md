Scope determines the accessibility (visibility) of variables.
JavaScript variables have 3 types of scope:
- Block scope
- Function scope
- Global scope

ES6 introduced two important new JavaScript keywords: `let` and `const`.
These two keywords provide Block Scope in JavaScript.
Variables declared inside a { } block cannot be accessed from outside the block:
```js
{  
  let x = 2;  
}  
// x can NOT be used here
```

Variables declared with the `var` keyword can NOT have block scope.
Variables declared inside a { } block can be accessed from outside the block.
```js
{  
  var x = 2;  
}  
// x CAN be used here
```

###### **Local Scope**
Variables declared within a JavaScript function, are LOCAL to the function:
```js
// code here can NOT use carName  
  
function myFunction() {  
  let carName = "Volvo";  
  // code here CAN use carName  
}  
  
// code here can NOT use carName
```

###### **Global Scope**
Variables declared Globally (outside any function) have Global Scope.
Global variables can be accessed from anywhere in a JavaScript program.
Variables declared with `var`, `let` and `const` are quite similar when declared outside a block.
```js
var x = 2;       // Global scope
let x = 2;       // Global scope
const x = 2;       // Global scope
```

###### **Global Variables in HTML**
With JavaScript, the global scope is the JavaScript environment.
In HTML, the global scope is the window object.
Global variables defined with the `var` keyword belong to the window object:
```js
var carName = "Volvo";  
// code here can use window.carName
```
Global variables defined with the `let` keyword do not belong to the window object:
```js
let carName = "Volvo";  
// code here can not use window.carName
```
