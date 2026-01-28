---
tags:
  - review
sr-due: 2026-06-10
sr-interval: 165
sr-ease: 290
---

---
**Binding** $-$ момент, когда метод или переменная привязывается к конкретной реализации.

###### **Раннее (static binding, compile-time binding)**
- Происходит на этапе компиляции.
- JVM уже знает, какой метод будет вызван.        
- Применяется к:        
        - `static`, `final` методам
        - перегрузке методов (method overloading)
- Быстрое, потому что не требует поиска во время выполнения.
        
###### **Позднее (dynamic binding, runtime binding)**    
- Определяется во время выполнения программы.
- JVM решает, какой метод вызвать, исходя из реального объекта, на который указывает ссылка.        
- Применяется к:    
    - переопределённым методам (method overriding)
    - полиморфизму
- Гибкое, но чуть медленнее.        

###### **Static binding (раннее связывание)**
```java
class Animal {
    private void privateMethod() {
        System.out.println("Приватный метод Animal");
    }

    static void staticMethod() {
        System.out.println("Статический метод Animal");
    }

    final void finalMethod() {
        System.out.println("Финальный метод Animal");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal.staticMethod(); // статическое связывание
    }
}
```

###### **Dynamic binding (позднее связывание)**
```java
class Animal {
    void sound() {
        System.out.println("Животное издаёт звук");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Собака лает");
    }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Dog(); // ссылка типа Animal, объект Dog
        a.sound(); // позднее связывание
    }
}
```
