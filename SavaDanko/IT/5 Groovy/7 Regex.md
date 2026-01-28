**Регулярные выражения (Regex)** — это шаблоны для поиска текста.
В Groovy регулярки — это объекты `Pattern` или `Matcher`, создаваемые удобным синтаксисом.
##### ==Как создать регулярку в Groovy==
- С помощью «slashy strings»:
```groovy
def pattern = /ab+c/
```
  
- Или **с `~`** — это создаёт объект `Pattern`:    
```groovy
def regex = ~/ab+c/
```

- Или через `Pattern.compile` (как в Java):  
```groovy
def regex = Pattern.compile("ab+c")
```    

##### ==Сопоставление с регуляркой (Matching)==
Оператор `==~` — **полное совпадение** строки с шаблоном
```groovy
assert "abc" ==~ /ab+c/  // true
```

Метод `.matches()` — как в Java
```groovy
"12345".matches(/\d+/)  // true
```

##### ==Поиск вхождения (Partial match)==
- `=~` возвращает **Matcher**, можно искать совпадения:
```groovy
def m = "I love Groovy" =~ /Groovy/
if (m) println "Found!"  // true
```
  
##### ==Замена текста==
```groovy
def result = "abc123".replaceAll(/\d+/, "#")
println result  // abc#
```

##### ==Захватывающие группы (Capturing groups)==
```groovy
def m = "Price: $15.99" =~ /Price: \$(\d+)\.(\d+)/
if (m) {
    println "Dollars: ${m[0][1]}, Cents: ${m[0][2]}" // Dollars: 15, Cents: 99
}
```
