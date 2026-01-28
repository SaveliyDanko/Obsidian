Groovy использует **литералы списков** — квадратные скобки:
```groovy
def list = [1, 2, 3, 4]
```

Тип по умолчанию — `java.util.ArrayList`:
```groovy
assert list instanceof ArrayList
```

Смешанные типы также допустимы (динамическая типизация):
```groovy
def mixed = [1, "two", true, [nested: "map"]]
```

Можно явно задать тип:
```groovy
List<String> names = ["Alice", "Bob"]
```


###### **Добавление**
```groovy
def list = []
list << 1           // оператор "append"
list.add(2)
list.addAll([3, 4])
```

###### **Удаление**
```groovy
list.remove(1)      // удаляет по индексу
list -= 4           // удаляет по значению
```

###### **Доступ к элементам**
```groovy
def list = ['a', 'b', 'c']

println list[0]          // 'a'
println list[-1]         // 'c' — индексация с конца
list[1] = 'z'            // изменение значения
```

###### **Диапазоны и срезы**
```groovy
def list = [10, 20, 30, 40, 50]

println list[1..3]       // [20, 30, 40]
println list[0, 2, 4]    // [10, 30, 50]
```

###### **Проход по списку**
`each`
```groovy
list.each { println it }
```

`eachWithIndex`
```groovy
list.eachWithIndex { item, idx -> println "$idx: $item" }
```


###### **Фильтрация, трансформация и поиск**
`find`, `findAll`
```groovy
def list = [1, 2, 3, 4, 5]

def even = list.findAll { it % 2 == 0 }  // [2, 4]
def firstEven = list.find { it % 2 == 0 } // 2
```

`collect` — как `map()`
```groovy
def squares = list.collect { it * it } // [1, 4, 9, 16, 25]
```

###### **Сортировка и уникальность**
```groovy
def list = [5, 1, 4, 2, 3]

println list.sort()             // [1, 2, 3, 4, 5]
println list.unique()           // Удаляет дубликаты
```

Сортировка по компаратору:
```groovy
def names = ["Anna", "Bob", "Christina"]
names.sort { a, b -> b <=> a }  // обратная сортировка
```

###### **Полезные методы**

| Метод            | Описание                                  |
| ---------------- | ----------------------------------------- |
| `join(',')`      | Объединение элементов в строку            |
| `sum()`          | Суммирование чисел в списке               |
| `max()`, `min()` | Поиск максимального/минимального элемента |
| `reverse()`      | Обратный порядок элементов                |
| `flatten()`      | "Выравнивание" вложенных списков          |
