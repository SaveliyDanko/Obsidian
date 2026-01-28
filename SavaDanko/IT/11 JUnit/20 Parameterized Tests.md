**Parameterized Tests** — это тесты, которые позволяют запускать один и тот же тестовый метод несколько раз с разными входными данными.

Обычный тест (`@Test`) выполняется один раз.
`@ParameterizedTest`выполняется N раз — по числу переданных параметров.

Каждый прогон теста имеет своё значение:
- входные данные
- своё имя (можно настроить)
- свой отдельный отчёт
```java
@ParameterizedTest
@ValueSource(strings = {"Anna", "Bob", "Carol"})
void testIsNotEmpty(String name) {
    assertFalse(name.isEmpty());
}
```
Тест запустится 3 раза: для "Anna", "Bob", "Carol".

###### **Источники данных (sources)**
JUnit 5 предлагает гибкую систему источников входных данных:
`@ValueSource` — примитивы и строки
```java
@ValueSource(ints = {1, 2, 3, 10})
```
- strings
- ints
- longs
- doubles
- booleans
- classes

`@CsvSource` — несколько аргументов
```java
@ParameterizedTest
@CsvSource({
    "Anna, 4",
    "Bob, 3"
})
void testLength(String input, int expected) {
    assertEquals(expected, input.length());
}
```

`@CsvFileSource` — данные из файла
```java
@CsvFileSource(resources = "/names.csv", numLinesToSkip = 1)
```

`@EnumSource` — перебор значений enum
```java
@EnumSource(MyEnum.class)
```

`@MethodSource` — данные из метода
Самый гибкий вариант (вернуть Stream / List / Iterable):
```java
static Stream<String> names() {
    return Stream.of("test", "demo");
}

@ParameterizedTest
@MethodSource("names")
void testNames(String name) {}
```

`@ArgumentsSource` — свой собственный источник данных
Можно написать свой класс, который предоставляет аргументы.

###### **Настройка имени каждого запуска**
```java
@ParameterizedTest(name = "{index} => name={0}, length={1}")
@CsvSource({
    "Anna, 4",
    "Bob, 3"
})
```
Плейсхолдеры:
- `{index}` — номер запуска
- `{0}`, `{1}` — параметры
- `{arguments}` — всё сразу