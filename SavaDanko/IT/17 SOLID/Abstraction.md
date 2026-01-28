---
tags:
  - review
sr-due: 2026-03-10
sr-interval: 84
sr-ease: 270
---

---
It means hiding implementation details and showing only the essential features of an object.
- Focuses on what an object does rather than how it does it.
- Achieved in Java via:
    1. Abstract classes
    2. Interfaces

###### **Abstraction using Interfaces**
```java
interface Animal {
    void makeSound();
}

class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Bark");
    }
}

class Cat implements Animal {
    @Override
    public void makeSound() {
        System.out.println("Meow");
    }
}
```

