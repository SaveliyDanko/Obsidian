###### **Объявление Range**
Groovy позволяет создавать диапазоны с помощью операторов:

| Диапазон | Описание                        |
| -------- | ------------------------------- |
| `1..5`   | Закрытый диапазон (включает 5)  |
| `1..<5`  | Открытый диапазон (исключает 5) |

```groovy
def r1 = 1..5    // [1, 2, 3, 4, 5]
def r2 = 1..<5   // [1, 2, 3, 4]
```

###### **Тип диапазона: `IntRange` и `Range`**
```groovy
assert (1..5) instanceof IntRange
assert ('a'..'z') instanceof ObjectRange
```
Groovy автоматически подбирает тип диапазона:
- `IntRange` — для `int`, `long`
- `CharRange` / `ObjectRange` — для `char`, `String`, `Comparable`

###### **Итерация по Range**
```groovy
for (i in 1..3) {
    println "Итерация $i"
}
```
Или декларативно:
```groovy
(1..5).each { println it }
```

###### **Проверка принадлежности (`in`)**
```groovy
def range = 10..20

println 15 in range      // true
println 25 in range      // false
```
Можно использовать для валидации:
```groovy
if (score in 0..100) println "Оценка допустима"
```

###### **Работа с символами и строками**
Groovy поддерживает диапазоны не только чисел:
```groovy
def letters = 'a'..'d'
println letters.toList() // ['a', 'b', 'c', 'd']
```
Диапазоны `String` работают, если строки — односимвольные и реализуют `Comparable`.

###### **Обратные диапазоны**
```groovy
def down = 5..1
println down.toList()    // [5, 4, 3, 2, 1]
```
Можно использовать в `downto`:
```groovy
5.downto(1) { println it }
```

###### **Сравнение диапазонов**
```groovy
assert (1..5) == new IntRange(1, 5)
```
Можно проверять равенство, границы, использовать `.contains()`.

###### **Свойства и методы Range**
```groovy
def r = 10..15

println r.size()         // 6
println r.from           // 10
println r.to             // 15
println r.contains(12)   // true
```

###### **Применение в условиях и switch-case**
Диапазоны часто используются в логике условий:
```groovy
def temp = 37

switch (temp) {
    case 36..37:
        println "Норма"
        break
    case 38..40:
        println "Повышенная температура"
        break
    default:
        println "Вне диапазона"
}
```
