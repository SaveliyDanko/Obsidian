---
tags:
  - review
sr-due: 2026-02-15
sr-interval: 42
sr-ease: 230
---

---
**ObjectMapper** — это основной класс библиотеки Jackson, который отвечает за сериализацию (преобразование Java-объектов в JSON) и десериализацию (из JSON обратно в объекты).  

###### **Назначение**
ObjectMapper используется для:
- чтения JSON → Java-объекты / JsonNode
- записи Java-объектов → JSON (строка, файл, поток)
- настройки формата JSON (pretty print, правила сериализации/десериализации)
- работы с JSON-деревом
- конвертации объектов разных типов

###### **Десериализация**
- `readValue(String json, Class<T> valueType)` — JSON → объект.
- `readValue(File src, Class<T>)` — JSON-файл → объект.
- `readTree(String json)` — JSON → дерево `JsonNode`.

###### **Сериализация**
- `writeValueAsString(Object value)` — объект → JSON-строка.
- `writeValue(File file, Object value)` — объект → JSON-файл.
- `writerWithDefaultPrettyPrinter()` — включить красивый вывод.

###### **Работа с деревьями**
- `createObjectNode()` — создать пустой ObjectNode.
- `createArrayNode()` — создать пустой ArrayNode.