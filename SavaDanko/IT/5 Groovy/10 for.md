###### **Итерация по диапазонам**
Один из наиболее распространённых способов итерации в Groovy:
```groovy
for (i in 1..5) {
    println "Итерация $i"
}
```
Диапазон `1..5` включает обе границы.
Можно использовать открытый диапазон `1..<5`, который исключает правую границу.

###### **Итерация по коллекциям**
```groovy
def list = ["Java", "Groovy", "Kotlin"]

for (lang in list) {
    println "Язык: $lang"
}
```

```groovy
for (key, value in map) {
    println "$key = $value"
}
```

###### **Итерация с помощью методов коллекций**
```groovy
["a", "b", "c"].each { println it }
```

Или с индексом:
```groovy
["a", "b", "c"].eachWithIndex { item, index ->
    println "$index : $item"
}
```

```groovy
def map = [a: 1, b: 2, c: 3]

map.each { key, value ->
    println "$key => $value"
}
```

##### **Итерация с фильтрацией: `findAll` и `each`**
```groovy
(1..10).findAll { it % 2 == 0 }.each { println it }
```
Сначала выбираются только чётные числа.  
Затем по ним выполняется итерация.

###### **Итерация с `times`**
Для определённого числа повторов:
```groovy
5.times {
    println "Привет, мир!"
}
```

С индексом:
```groovy
5.times { i ->
    println "Итерация $i"
}
```

###### **Итерация с `upto` и `downto`**
```groovy
1.upto(3) { println it }    // 1 2 3
3.downto(1) { println it }  // 3 2 1
```

###### **Итерация по строкам и массивам**
```groovy
for (ch in "Groovy") {
    println ch
}
```

Или по массиву:
```groovy
def arr = [10, 20, 30] as int[]
for (n in arr) {
    println n
}
```
