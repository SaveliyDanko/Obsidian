**Dynamic Tests** — это механизм, позволяющий создавать тесты на лету (во время выполнения), а не заранее, как обычные `@Test`-методы.

Это даёт мощный и гибкий способ генерировать тесты:
- на основе входных данных
- коллекций
- файлов
- API-ответов
- случайных значений
- заранее неизвестного количества сценариев

###### **Что такое Dynamic Test простыми словами?**
Обычные тесты — статические. Количество тестов известно до запуска.
Dynamic Test — это тесты, создаваемые программно, в коде, при запуске тестового класса.

Например: есть список входных значений, и ты хочешь сгенерировать по тесту для каждого. Dynamic Test создаёт тесты по этому списку.
```java
@TestFactory
Collection<DynamicTest> dynamicTests() {
    return List.of(
        DynamicTest.dynamicTest("Test 1", () -> assertTrue(1 < 2)),
        DynamicTest.dynamicTest("Test 2", () -> assertEquals(4, 2 + 2))
    );
}
```
Каждый `DynamicTest`:
- имеет название (отображается в отчётах),
- содержит тестовый код (`Executable`).

```java
@TestFactory
Stream<DynamicTest> testStrings() {
    List<String> inputs = List.of("a", "bb", "ccc");

    return inputs.stream()
        .map(str -> DynamicTest.dynamicTest(
            "Length test for: " + str,
            () -> assertTrue(str.length() > 0)
        ));
}
```
Сгенерируется 3 отдельных теста.