###### **Чтение одной строки из консоли**
```groovy
print "Введите ваше имя: "
def name = System.console().readLine()
println "Привет, $name!"
```
Этот способ работает **только в реальной консоли**, а не в IDE (например, IntelliJ IDEA может возвращать `null`).

###### **Альтернатива (универсально работает и в IDE):**
```groovy
print "Введите ваше имя: "
def name = System.in.newReader().readLine()
println "Привет, $name!"
```
Работает везде, в том числе при запуске скрипта через IDE или `groovy script.groovy`

###### **Ввод чисел и преобразование типов**
```groovy
print "Введите возраст: "
def age = System.in.newReader().readLine() as Integer
println "Через год вам будет ${age + 1}"
```
Поддерживаются: `as Integer`, `as Double`, `as BigDecimal` и т.д.

###### **Цикл ввода до нужного значения**
```groovy
def reader = System.in.newReader()
def number

while (true) {
    print "Введите число больше 10: "
    number = reader.readLine() as Integer
    if (number > 10) break
    println "Слишком маленькое число!"
}
println "Спасибо, вы ввели $number"
```

###### **Ввод нескольких значений через split**
```groovy
print "Введите 3 числа через пробел: "
def input = System.in.newReader().readLine()
def numbers = input.split().collect { it as Integer }

println "Сумма: ${numbers.sum()}"
```

###### **Ввод с паролем (без отображения)**
```groovy
def password = System.console()?.readPassword("Введите пароль: ")
println "Введённый пароль: ${password?.join()}"
```
`readPassword()` работает только в **реальной консоли** — в IDE вернёт `null`
