Trait — это **особый тип**, похожий на интерфейс, но позволяющий:
- Определять методы с реализацией (включая приватные).
- Добавлять поля (с ограничениями).    
- Использовать другое поведение по композиции (`self-type` pattern).
- Наследоваться множественно, без конфликтов классов.
    

###### **Объявление и использование Trait**
```groovy
trait Greetable {
    String greet(String name) {
        "Hello, $name"
    }
}

class Person implements Greetable {}

def p = new Person()
println p.greet("Alice")  // Hello, Alice
```
Класс `Person` "наследует" поведение, описанное в `Greetable`.

###### **Особенности Traits**
Поддерживают множественное "наследование":
```groovy
trait A { String foo() { "A" } }
trait B { String bar() { "B" } }

class C implements A, B {}

println new C().foo()  // A
println new C().bar()  // B
```

###### **Можно вызывать `super` внутри трейта:**
```groovy
trait Logger {
    String log(String msg) { "LOG: $msg" }
}

trait TimestampLogger extends Logger {
    String log(String msg) {
        super.log("${new Date()}: $msg")
    }
}

class Service implements TimestampLogger {}

println new Service().log("Start")  
```

###### **Можно реализовывать приватные методы:**
```groovy
trait Secure {
    private boolean checkAuth() { true }

    String run() {
        if (checkAuth()) "Allowed" else "Denied"
    }
}
```

###### **Поля в Trait**
Traits могут иметь свойства (с `@groovy.transform.Field`) и использовать `private`/`public` поля, но:
- Поля не могут быть final.
- При использовании в классах дублируются для каждого трейта, а не объединяются.
```groovy
trait Counter {
    int count = 0
    void increment() { count++ }
}

class MyCounter implements Counter {}

def c = new MyCounter()
c.increment()
println c.count  // 1
```

---

###### **Конфликт при дублировании методов**
Если несколько трейтов реализуют одинаковый метод — порядок важен:
```groovy
trait A { String who() { "A" } }
trait B { String who() { "B" } }

class C implements A, B {}

println new C().who()  // B — последний wins
```

Можно явно указать, какой метод вызвать:
```groovy
class D implements A, B {
    String who() { A.super.who() + " + " + B.super.who() }
}
println new D().who()  // A + B
```

###### **Runtime внедрение трейтов (`withTraits`)**
Позволяет динамически "добавить" поведение объекту без модификации класса:
```groovy
trait Speaker { String speak() { "I can speak!" } }

class Dog {}

def d = new Dog().withTraits(Speaker)
println d.speak()  // I can speak!
```
