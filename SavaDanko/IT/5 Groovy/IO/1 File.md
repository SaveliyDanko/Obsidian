###### **Создание объекта `File`**
```groovy
def file = new File('example.txt')
```
- Это просто объект, представляющий файл `example.txt` в текущей директории
- Файл пока не обязательно существует

###### **Создание нового файла вручную**
```groovy
def newFile = new File('notes.txt')
newFile.createNewFile()
```

###### **Запись в файл**
Перезапись (удаляет старое содержимое):
```groovy
file.text = 'Hello, Groovy!'
```

Добавление текста (append):
```groovy
file << '\nAnother line'
```

С использованием `withWriter` (автоматически закрывает ресурс):
```groovy
file.withWriter { writer ->
    writer.writeLine('Line 1')
    writer.writeLine('Line 2')
}
```

###### **Чтение из файла**
Весь текст сразу:
```groovy
def content = file.text
println content
```

Построчное чтение:
```groovy
file.eachLine { line ->
    println ">> $line"
}
```

С доступом к номеру строки:
```groovy
file.eachLine { line, number ->
    println "$number: $line"
}
```

С использованием `withReader`:
```groovy
file.withReader { reader ->
    reader.eachLine { line ->
        println line
    }
}
```

###### **Удаление файла**
```groovy
file.delete()
```

###### **Работа с директориями**
```groovy
def dir = new File('data')
dir.mkdirs() // создаёт директорию и все родительские, если нужно

dir.eachFile { f ->
    println f.name
}
```

###### **Проверка существования файла**
```groovy
if (file.exists()) {
    println "Файл существует"
}
```

###### **Вложенные директории**
Создание вложенной структуры директорий (как `mkdir -p` в Linux):
```groovy
new File('project/src/main/groovy').mkdirs()
```

###### **Cоздание дерева проекта**
```groovy
def structure = [
    'project/src/main/groovy',
    'project/src/main/resources',
    'project/src/test/groovy',
    'project/docs',
    'project/build'
]

structure.each { path ->
    def dir = new File(path)
    if (dir.mkdirs()) {
        println "Создано: $path"
    } else {
        println "Уже существует или ошибка: $path"
    }
}
```
