#java 

---
**Generics** позволяют работать с типами данных как с параметрами.  

#### Без Generics (до Java 5)
```java
List list = new ArrayList();
list.add("Hello");
String s = (String) list.get(0); // ❗ нужно приведение типа (кастинг)
```

#### С Generics (Java 5+)
```java
List<String> list = new ArrayList<>();
list.add("Hello");
String s = list.get(0); // ✅ безопасно и без кастинга
```


#### ==Обобщённый класс==
```java
public class Box<T> {
    private T value;

    public void set(T value) {
        this.value = value;
    }

    public T get() {
        return value;
    }
}
```

Использование:
```java
Box<String> stringBox = new Box<>();
stringBox.set("Hello");

Box<Integer> intBox = new Box<>();
intBox.set(123);
```
Здесь `T` — параметр типа, который подставляется при создании экземпляра.

#### ==Обобщённый метод==
```java
public class Util {
    public static <T> void print(T value) {
        System.out.println(value);
    }
}
```

Использование:
```java
Util.print("Text");     // String
Util.print(42);         // Integer
Util.print(3.14);       // Double
```

#### ==Ограничения (bounded generics)==
Можно ограничивать допустимые типы:
```java
class Animal {}
class Dog extends Animal {}

public class Zoo<T extends Animal> {
    T resident;
}
```
Теперь `Zoo<String>` — ❌ ошибка  
А вот `Zoo<Dog>` — ✅ ок

#### ==Wildcards (`?`)==
Иногда ты не знаешь точный тип, но хочешь поддерживать "что-то совместимое".
```java
public void printAll(List<?> list) {
    for (Object obj : list) {
        System.out.println(obj);
    }
}
```

| Синтаксис       | Описание                     |
| --------------- | ---------------------------- |
| `<?>`           | Любой тип                    |
| `<? extends T>` | Любой подкласс (или сам `T`) |
| `<? super T>`   | Любой надкласс (или сам `T`) |
