---
tags:
  - review
sr-due: 2026-03-30
sr-interval: 63
sr-ease: 250
---

---
[[6.1 @Configuration]]
[[6.2 @Bean]]

```java
@Configuration
public class AppConfig {

    @Bean
    public Engine engine() {
        return new Engine("V8");
    }

    @Bean
    public Car car() {
        Car car = new Car(engine());  // передаём зависимость
        car.setColor("red");          // настраиваем бин
        return car;
    }
}
```

```java
public class App {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        Car car = context.getBean(Car.class);
        car.drive();
    }
}
```

