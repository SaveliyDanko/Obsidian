---
tags:
  - review
sr-due: 2026-01-31
sr-interval: 23
sr-ease: 210
---
---
[Article](https://www.baeldung.com/jpa-many-to-many)

---
A relationship is a connection between two types of entities. In the case of a many-to-many relationship, both sides can relate to multiple instances of the other side. Note that it’s possible for entity types to be in a relationship with themselves.

Let’s take the example of students marking the courses they like.

A student can like **many** courses, and **many** students can like the same course:
![[Pasted image 20251221233647.png]]

As we know, in RDBMSs we can create relationships with foreign keys. Since both sides should be able to reference the other, we need to create a separate table to hold the foreign keys:
![[Pasted image 20251221233722.png]]
Such a table is called a **join table.** In a join table, the combination of the foreign keys will be its composite primary key.

---
Modeling a many-to-many relationship with POJOs is easy. We should include a Collection in both classes, which contains the elements of the others.
```java
@Entity
class Student {
    @Id
    Long id;

    @ManyToMany
    Set<Course> likedCourses;
}

@Entity
class Course {

    @Id
    Long id;

    @ManyToMany
    Set<Student> likes;
}
```

Additionally, we have to configure how to model the relationship in the RDBMS.
```java
@ManyToMany
@JoinTable(
  name = "course_like", 
  joinColumns = @JoinColumn(name = "student_id"), 
  inverseJoinColumns = @JoinColumn(name = "course_id"))
Set<Course> likedCourses;
```

On the target side, we only have to provide the name of the field, which maps the relationship.
```java
@ManyToMany(mappedBy = "likedCourses")
Set<Student> likes;
```