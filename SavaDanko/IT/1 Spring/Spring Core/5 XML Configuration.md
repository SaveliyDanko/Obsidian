---
tags:
  - review
sr-due: 2026-04-06
sr-interval: 69
sr-ease: 250
---

---
```java
public class Engine {
    private String type;

    public Engine(String type) {
        this.type = type;
    }

    public String getType() {
        return type;
    }
}
```

```java
public class Car {
    private Engine engine;
    private String color;

    public Car(Engine engine) {
        this.engine = engine;
    }

    public void setColor(String color) {
        this.color = color;
    }

    public void drive() {
        System.out.println("Driving a " + color + " car with " + engine.getType() + " engine.");
    }
}
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans 
                           http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="engine" class="com.example.Engine">
        <constructor-arg value="V8" />
    </bean>

    <bean id="car" class="com.example.Car">
        <constructor-arg ref="engine" />
        <property name="color" value="red"/>
    </bean>

</beans>
```

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

        Car car = (Car) context.getBean("car");
        car.drive();

		context.cloase();
    }
}
```
