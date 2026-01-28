Groovy поддерживает **литералы мап** через синтаксис `key: value`.
```groovy
def person = [name: "Alice", age: 30]
```
По умолчанию создаётся `LinkedHashMap` (сохранение порядка).  
Ключи по умолчанию — `String`, но могут быть и другими объектами:
```groovy
def map = [(1): "one", (2): "two"] // ключи-числа
```

###### **Доступ к значениям**
Через `[]`-нотацию:
```groovy
println person["name"]    // Alice
```

Через точку:
```groovy
println person.name       // Alice
```

Безопасный доступ:
```groovy
println person["email"]           // null
println person?.email             // null (без NPE)
```

###### **Изменение и добавление элементов**
```groovy
person["email"] = "alice@example.com"
person.age = 31

person << [city: "Paris"]        // оператор расширения
```

###### **Удаление элементов**
```groovy
person.remove("email")
person -= "city"
```

###### **Проход по Map**
`each`
```groovy
person.each { key, value ->
    println "$key = $value"
}
```

`eachWithIndex`
```groovy
person.eachWithIndex { entry, i ->
    println "${i}: ${entry.key} -> ${entry.value}"
}
```

###### **Фильтрация и преобразование**
```groovy
def adults = [John: 34, Mary: 17, Bob: 42]
def filtered = adults.findAll { k, v -> v >= 18 }

def names = adults.collect { k, v -> k.toUpperCase() }
```

###### **Проверка наличия ключей и значений**
```groovy
if (person.containsKey("name")) println "Есть имя"
if ("Alice" in person.values()) println "Нашли Алису"
```

###### **Доступ к ключам и значениям**
```groovy
println person.keySet()       // [name, age]
println person.values()       // [Alice, 30]
println person.entrySet()     // [name=Alice, age=30]
```

###### **Объединение Map**
```groovy
def map1 = [a: 1, b: 2]
def map2 = [b: 3, c: 4]

def result = map1 + map2
println result  // [a:1, b:3, c:4] (map2 перезаписывает ключи map1)
```
