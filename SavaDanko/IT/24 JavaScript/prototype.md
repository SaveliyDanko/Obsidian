Каждая функция в JavaScript автоматически получает свойство `prototype`. Это объект, который используется для наследования свойств и методов другими объектами, созданными через `new`.
```js
function Person(name) {
  this.name = name;
}

Person.prototype.sayHello = function () {
  console.log(`Привет, меня зовут ${this.name}`);
};

const user1 = new Person("Alice");
const user2 = new Person("Bob");

user1.sayHello(); // Привет, меня зовут Alice
user2.sayHello(); // Привет, меня зовут Bob
```
Оба объекта (`user1`, `user2`) не содержат метод `sayHello` внутри себя, они находят его через `Person.prototype`.

###### **Прототипное наследование**
В JS у каждого объекта есть скрытое свойство `[[Prototype]]` (в браузерах доступно как `__proto__`), которое указывает на другой объект.
```js
console.log(user1.__proto__ === Person.prototype); // true
```
Когда мы обращаемся к `user1.sayHello`, движок ищет свойство:
1. В объекте `user1`.
2. Если не найдено — в `user1.__proto__` (то есть `Person.prototype`).
3. Если и там нет — идёт выше по цепочке (`Object.prototype`).
4. Если в конце (`null`) не найдено — возвращает `undefined`.
Это называется цепочка прототипов (prototype chain).

###### **Добавление методов на лету**
Можно расширять прототип даже после создания объектов:
```js
Person.prototype.sayBye = function () {
  console.log(`${this.name} говорит: Пока!`);
};

user1.sayBye(); // Alice говорит: Пока!
user2.sayBye(); // Bob говорит: Пока!
```
Оба объекта получили новый метод.

###### **Наследование через `prototype`**
```js
function Animal(name) {
  this.name = name;
}

Animal.prototype.speak = function () {
  console.log(`${this.name} издаёт звук`);
};

function Dog(name) {
  Animal.call(this, name); // вызываем конструктор родителя
}

// наследуем прототип Animal
Dog.prototype = Object.create(Animal.prototype);
Dog.prototype.constructor = Dog;

Dog.prototype.speak = function () {
  console.log(`${this.name} лает`);
};

const dog = new Dog("Шарик");
dog.speak(); // Шарик лает
```

---

###### **Современный синтаксис (ES6 `class`)**
Классы в JavaScript — это синтаксический сахар над `prototype`.
```js
class Person {
  constructor(name) {
    this.name = name;
  }

  sayHello() {
    console.log(`Привет, я ${this.name}`);
  }
}

const p = new Person("Eve");
p.sayHello(); // Привет, я Eve
```
Под капотом всё то же самое: `sayHello` хранится в `Person.prototype`.