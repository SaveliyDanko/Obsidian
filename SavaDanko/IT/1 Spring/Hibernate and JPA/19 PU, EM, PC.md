---
tags:
  - review
sr-due: 2026-02-11
sr-interval: 58
sr-ease: 250
---

---
###### **Persistence Unit**
PersistenceUnit — это набор настроек JPA + список сущностей, описанный в `persistence.xml`.
```xml
<persistence xmlns="http://xmlns.jcp.org/xml/ns/persistence"
             version="2.1">
    <persistence-unit name="myPu" transaction-type="RESOURCE_LOCAL">
        <provider>org.hibernate.jpa.HibernatePersistenceProvider</provider>

        <!-- Классы-сущности -->
        <class>com.example.User</class>
        <class>com.example.Order</class>

        <!-- Настройки подключения -->
        <properties>
            <property name="javax.persistence.jdbc.url" value="jdbc:postgresql://localhost:5432/mydb"/>
            <property name="javax.persistence.jdbc.user" value="postgres"/>
            <property name="javax.persistence.jdbc.password" value="secret"/>

            <!-- Настройки Hibernate -->
            <property name="hibernate.hbm2ddl.auto" value="update"/>
            <property name="hibernate.show_sql" value="true"/>
        </properties>
    </persistence-unit>
</persistence>
```
Имя `myPu` потом используется для создания `EntityManagerFactory`.

###### **EntityManager**
EntityManager — главный интерфейс JPA:
- управляет сущностями (persist, merge, remove, find)
- работает с БД (запросы, транзакции)
- внутри содержит PersistenceContext
В Java SE обычно:
```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("myPu");
EntityManager em = emf.createEntityManager();

em.getTransaction().begin();

User user = new User();
user.setName("Alice");

em.persist(user);   // user -> Managed, будет INSERT при commit

em.getTransaction().commit();

em.close();
emf.close();
```
В Spring / Jakarta EE `EntityManager` чаще всего внедряется:
```java
// Spring
@Repository
public class UserRepository {

    @PersistenceContext
    private EntityManager em;

    public User find(Long id) {
        return em.find(User.class, id);
    }

    public void save(User user) {
        em.persist(user);
    }
}
```

###### **PersistenceContext**
PersistenceContext — это 1-й уровень кэша + набор Managed-сущностей, связанный с конкретным `EntityManager`.
Важно:
- в рамках одного `EntityManager` одна и та же строка БД = один Java-объект
- изменения в Managed-объектах автоматически попадут в БД при `flush()/commit()`
```java
em.getTransaction().begin();

User u1 = em.find(User.class, 1L);
User u2 = em.find(User.class, 1L);

System.out.println(u1 == u2); // true — один объект в persistence context

u1.setName("Bob");            // просто меняем поле

// Никакого em.update() нет — JPA сам увидит изменение
em.getTransaction().commit(); // тут будет UPDATE

em.close();                   // persistence context уничтожен
```

---
```java
public class Main {
    public static void main(String[] args) {
        EntityManagerFactory emf =
                Persistence.createEntityManagerFactory("myPu");
        EntityManager em = emf.createEntityManager();

        // CREATE
        em.getTransaction().begin();
        User user = new User();
        user.setName("Alice");
        em.persist(user);                // New -> Managed
        em.getTransaction().commit();    // INSERT

        // READ + UPDATE
        em.getTransaction().begin();
        User u = em.find(User.class, user.getId()); // Managed
        u.setName("Alice Updated");                 // просто меняем поле
        em.getTransaction().commit();               // UPDATE

        // DELETE
        em.getTransaction().begin();
        User toDelete = em.find(User.class, user.getId());
        em.remove(toDelete);                        // Managed -> Removed
        em.getTransaction().commit();               // DELETE

        em.close();
        emf.close();
    }
}
```
