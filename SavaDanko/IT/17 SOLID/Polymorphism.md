---
tags:
  - review
sr-due: 2026-06-14
sr-interval: 168
sr-ease: 290
---
---
[Статья про Полиморфизм](https://medium.com/devschacht/polymorphism-207d9f9cd78)

---
###### **Ad-hoc polymorphism**
- Means: “same name, different implementations depending on argument types.”
- Realized by function/method overloading and operator overloading.
- The compiler decides which function to call based on argument types.
```java
class Printer {
    void print(int x) {
        System.out.println("int: " + x);
    }
    void print(String s) {
        System.out.println("String: " + s);
    }
}
```

###### **Subtype polymorphism**
- Means: “if X is a subtype of Y, then X can be used wherever Y is expected.”
- This is the classic OOP polymorphism (inheritance + overriding).
- Realized in Java through inheritance (`extends`) and interfaces (`implements`).
```java
class Animal {
    void makeSound() { System.out.println("Some sound"); }
}

class Dog extends Animal {
    @Override
    void makeSound() { System.out.println("Bark"); }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Dog(); // subtype polymorphism
        a.makeSound(); // Bark
    }
}
```

###### **Parametric polymorphism**
- Means: “code written once can work for any type.”
- In Java, realized through generics (`<T>`).
- The exact type is not known until the class/method is instantiated.
```java
class Box<T> {
    private T value;
    void set(T value) { this.value = value; }
    T get() { return value; }
}

public class Main {
    public static void main(String[] args) {
        Box<Integer> intBox = new Box<>();
        intBox.set(123);
        System.out.println(intBox.get()); // 123

        Box<String> strBox = new Box<>();
        strBox.set("hello");
        System.out.println(strBox.get()); // hello
    }
}
```
