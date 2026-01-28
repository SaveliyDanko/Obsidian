---
tags:
  - review
sr-due: 2026-08-24
sr-interval: 226
sr-ease: 310
---

---
- Создание новых классов на основе существующих.
- Позволяет переиспользовать код и расширять функциональность.
```java
class Vehicle {
    void move() {
        System.out.println("Транспорт движется");
    }
}

class Car extends Vehicle {
    @Override
    void move() {
        System.out.println("Машина едет по дороге");
    }
}
```