#js 

---
[Object](https://learn.javascript.ru/object)
[Objects](https://www.w3schools.com/jsref/jsref_obj_object.asp)


---
###### **JavaScript Objects**
Objects are variables. But objects can contain many values.
```js
const car = {type:"Fiat", model:"500", color:"white"};
```
It is a common practice to declare objects with the const keyword.

###### **JavaScript Object Definition**
Creating a JavaScript Object:
```js
const person = {firstName:"John", lastName:"Doe", age:50, eyeColor:"blue"};
```

Create a new JavaScript object using `new Object()`:
```js
const person = new Object();  
  
// Add Properties  
person.firstName = "John";  
person.lastName = "Doe";  
person.age = 50;  
person.eyeColor = "blue";
```

###### **Object Properties**
The named values, in JavaScript objects, are called properties.

###### **Accessing Object Properties**
```js
objectName.propertyName
objectName["propertyName"]
```

###### **JavaScript Object Methods**
Methods are actions that can be performed on objects.
Methods are function definitions stored as property values.
```js
const person = {  
  firstName: "John",  
  lastName : "Doe",  
  id       : 5566,  
  fullName : function() {  
    return this.firstName + " " + this.lastName;  
  }  
};
```
In the example above, `this` refers to the person object:
- `this.firstName` means the `firstName` property of person.
- `this.lastName` means the `lastName` property of person.

###### **Accessing JavaScript Properties**
```js
// objectName.property  
let age = person.age;

//objectName["property"]  
let age = person["age"];

//objectName[expression]
let age = person[x];
```

###### **Adding New Properties**
You can add new properties to an existing object by simply giving it a value:
```js
person.nationality = "English";
```

###### **Deleting Properties**
The `delete` keyword deletes a property from an object:
```js
const person = {
  firstName: "John",
  lastName: "Doe",
  age: 50,
  eyeColor: "blue"
};

delete person.age;
```

###### **Nested Objects**
Property values in an object can be other objects:
```js
myObj = {
  name:"John",
  age:30,
  myCars: {
    car1:"Ford",
    car2:"BMW",
    car3:"Fiat"
  }
}
```
You can access nested objects using the dot notation or the bracket notation:
```js
myObj.myCars.car2;
myObj.myCars["car2"];
```

###### **Accessing Object Methods**
You access an object method with the following syntax:
```js
objectName.methodName()
```
If you invoke the fullName property with (), it will execute as a function:
```js
name = person.fullName();
```
If you access the fullName property without (), it will return the function definition:
```js
name = person.fullName;
```

###### **Adding a Method to an Object**
Adding a new method to an object is easy:
```js
person.name = function () {  
  return this.firstName + " " + this.lastName;  
};
```

###### **Displaying Object Properties**
The properties of an object can be displayed as a string:
```js
// Create an Object
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

// Display Properties
document.getElementById("demo").innerHTML =
person.name + "," + person.age + "," + person.city;
```

The properties of an object can be collected in a loop:
```js
// Create an Object
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

// Build a Text
let text = "";
for (let x in person) {
  text += person[x] + " ";
};

// Display the Text
document.getElementById("demo").innerHTML = text;
```

`Object.values()` creates an array from the property values:
```js
// Create an Object
const person = {
  name: "John",
  age: 30,
  city: "New York"
};

// Create an Array
const myArray = Object.values(person);

// Display the Array
document.getElementById("demo").innerHTML = myArray;
```

`Object.entries()` makes it simple to use objects in loops:
```js
const fruits = {Bananas:300, Oranges:200, Apples:500};  
  
let text = "";  
for (let [fruit, value] of Object.entries(fruits)) {  
  text += fruit + ": " + value + "<br>";  
}
```

JavaScript objects can be converted to a string with JSON method `JSON.stringify()`.
`JSON.stringify()` is included in JavaScript and supported in all major browsers.
```js
// Create an Object  
const person = {  
  name: "John",  
  age: 30,  
  city: "New York"  
};  
  
// Stringify Object  
let myString = JSON.stringify(person);  
  
// Display String  
document.getElementById("demo").innerHTML = myString;
```

###### **Object Constructors**
Sometimes we need to create many objects of the same type.
To create an object type we use an object constructor function.
It is considered good practice to name constructor functions with an upper-case first letter.

```js
function Person(first, last, age, eye) {  
  this.firstName = first;  
  this.lastName = last;  
  this.age = age;  
  this.eyeColor = eye;  
}
```
In the constructor function, `this` has no value.
The value of `this` will become the new object when a new object is created.

Now we can use `new Person()` to create many new Person objects:
```js
const myFather = new Person("John", "Doe", 50, "blue");  
const myMother = new Person("Sally", "Rally", 48, "green");  
const mySister = new Person("Anna", "Rally", 18, "green");
```

A value given to a property will be a default value for all objects created by the constructor:
```js
function Person(first, last, age, eyecolor) {
  this.firstName = first;
  this.lastName = last;
  this.age = age;
  this.eyeColor = eyecolor;
  this.nationality = "English";
}
```

###### **Object.assign()**
The `Object.assign()` method copies properties from one or more source objects to a target object.
```js
Object.assign(target, source(s))
```
Parameters:
- `target` - Required | An existing object.
- `source` - Required | One or more sources.

Return Value:
- `Object` - 	The target object.

###### **Object constructor**
The `constructor` property returns the function that created the Object prototype.
```js
object.constructor
```
Return Value:
```js
function Object() { [native code] }
```

###### **Object.keys()**
The `Object.keys()` method returns an array with the keys of an object.
The `Object.keys()` method does not change the original object.
```js
Object.keys(object)
```
- `object` - An iterable object.
Return Value:
- `Array` - An array containing the keys of the object.

###### **Object.values()**
The `Object.values()` method returns an array of the property values of an object.
The `Object.values()` method does not change the original object.
```js
Object.values(object)
```
- `object` - An object.
Return Value:
- `Array` - An iterable array of the object's property values.

###### **Object.entries()**
The `Object.entries()` method returns an array of the key/value pairs of an object.
The `Object.entries()` method does not change the original object.
The methods above return an Iterable (enumerable array).
```js
Object.values(object)
```
- `object` - An object.
Return Value:
- `Array` - An iterable array of the object's key/value pairs.

```js
const fruits = {Bananas:300, Oranges:200, Apples:500};

let text = "";
for (let [fruit, value] of Object.entries(fruits)) {
  text += fruit + ": " + value + "<br>";
}
```

###### **Object toString()**
The `toString()` method returns an object as a string.
The `toString()` method returns `[object Object]` if it cannot return a string.
`Object.toString()` always returns the object constructor.
The `toString()` method does not change the original object.
```js
object.toString()
```
Return Value:
- A string representing the object.

###### **Object valueOf()**
The `valueOf()` method returns the primitive value of an object.
If the object has no primitive value, `valueOf()` returns the object itself.
The `valueOf()` method does not change the original object.
```js
object.valueOf()
```


###### **Проверка существования свойства, оператор `in`**
- Оператор `in` проверяет, существует ли свойство в объекте:
  ```javascript
  let user = { name: "John", age: 30 };
  alert("age" in user); // true
  alert("blabla" in user); // false
  ```

- Отличие от `undefined`: если свойству присвоено значение `undefined`, оператор `in` всё равно вернёт `true`:
  ```javascript
  let obj = { test: undefined };
  alert("test" in obj); // true
  ```
