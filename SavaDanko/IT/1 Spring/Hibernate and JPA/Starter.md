Самый простой способ — использовать `Spring Boot` + `Spring Data JPA` + `H2` (встроенная БД).

Создаем проект через https://start.spring.io
Выбираем:
- Project: Gradle - Groovy
- Language: Java
- Spring Boot: last stable
- Dependencies:  
	- Spring Web  
	- Spring Data JPA  
	- H2 Database

###### **Структура проекта**
```
demo/
 ├─ src/main/java/com/example/demo/
 │   ├─ DemoApplication.java
 │   ├─ domain/
 │   │    └─ Person.java
 │   ├─ repository/
 │   │    └─ StudentRepository.java
 │   └─ runner/
 │        └─ DataLoader.java
 └─ src/main/resources/
      └─ application.properties
```

###### **Создаём сущность (Entity)**
```java
package com.example.demo.domain;  
  
import jakarta.persistence.*;  
import lombok.Getter;  
import lombok.NoArgsConstructor;  
import lombok.NonNull;  
import lombok.RequiredArgsConstructor;  
  
@Entity  
@Table(name = "persons")  
@Getter  
@NoArgsConstructor  
@RequiredArgsConstructor  
public class Person {  
  
    @Id  
    @GeneratedValue(strategy = GenerationType.IDENTITY)  
    private Long id;  
  
    @NonNull  
    private String name;  
  
    @NonNull  
    private Integer age;  
}
```

###### **Репозиторий**
```java
package com.example.demo.repository;  
  
import com.example.demo.domain.Person;  
import org.springframework.data.jpa.repository.JpaRepository;  
  
public interface PersonRepository extends JpaRepository<Person, Long> {  
}
```

###### **Конфигурация JPA и БД**
```java
# === H2 DATABASE ===
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# === JPA / Hibernate ===
spring.jpa.hibernate.ddl-auto=create-drop
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true

# === H2 console ===
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
```

###### **Добавим тестовый запуск (CommandLineRunner)**
```java
package com.example.demo.runner;  
  
import com.example.demo.domain.Person;  
import com.example.demo.repository.PersonRepository;  
import org.springframework.boot.CommandLineRunner;  
import org.springframework.stereotype.Component;  
  
@Component  
public class DataLoader implements CommandLineRunner {  
  
    private final PersonRepository personRepo;  
  
    public DataLoader(PersonRepository repo) {  
        this.personRepo = repo;  
    }  
  
    @Override  
    public void run(String... args) {  
        personRepo.save(new Person("Alice", 20));  
        personRepo.save(new Person("Bob", 22));  
    }  
}
```

###### **Открой H2 Console**
```bash
http://localhost:8080/h2-console
```

