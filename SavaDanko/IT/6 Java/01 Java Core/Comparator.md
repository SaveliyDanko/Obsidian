#java 

---
**`Comparator<T>`** — это интерфейс, который определяет, как сравнивать два объекта между собой.

##### Интерфейс `Comparator<T>`
```java
@FunctionalInterface
public interface Comparator<T> {
    int compare(T o1, T o2);
}
```
- Возвращает:
    - `0` — если равны
    - `> 0` — если `o1 > o2`
    - `< 0` — если `o1 < o2`

| Метод                           | Описание                    |
| ------------------------------- | --------------------------- |
| `Comparator.comparing(...)`     | Сравнение по полю           |
| `Comparator.thenComparing(...)` | Добавление второго критерия |
| `Comparator.reversed()`         | Обратный порядок            |
| `(a, b) -> ...`                 | Лямбда-выражение            |

### Cортировка с лямбдой
```java
List<Person> people = new ArrayList<>(List.of(
    new Person("Alice", 30),
    new Person("Bob", 25),
    new Person("Charlie", 30)
));

people.sort((p1, p2) -> Integer.compare(p1.getAge(), p2.getAge()));
```

##### `Comparator.comparing()`
```java
people.sort(
    Comparator.comparing(Person::getAge)
              .thenComparing(Person::getName)
);
```

##### Обратный порядок
```java
people.sort(
    Comparator.comparing(Person::getAge).reversed()
);
```

##### Передача `Comparator` в `TreeSet`
```java
Set<Person> set = new TreeSet<>(
    Comparator.comparing(Person::getName)
);
```