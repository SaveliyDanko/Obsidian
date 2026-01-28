---
tags:
  - review
sr-due: 2026-02-16
sr-interval: 43
sr-ease: 230
---
---
**Смотреть примеры в репозитории**

---
**ObjectNode** — это класс Jackson, представляющий JSON-объект как часть дерева `JsonNode`.
Он содержит набор пар "ключ → значение" и позволяет читать, изменять и создавать JSON-объекты вручную. Это изменяемый (mutable) узел.

###### **Назначение**
ObjectNode используется, когда нужно:
- программно собирать JSON-объект
- изменять существующее дерево JSON
- добавлять, удалять, заменять поля в JSON
- строить динамические структуры без создания POJO-моделей

###### **Добавление и изменение полей**
- `put(String field, String/number/boolean value)`  
    Добавляет или заменяет примитивное значение.
    
- `set(String field, JsonNode value)`  
    Универсальная установка любого узла.
    
- `putNull(String field)`  
    Устанавливает `null`.
    
- `putArray(String field)`  
    Создаёт и привязывает новый `ArrayNode`.

###### **Удаление полей**
- `remove(String fieldName)` — удалить одно поле.
- `remove(Collection<String> fieldNames)` — удалить несколько.    
- `removeAll()` — очистить весь объект.

###### **Создание вложенных структур**
- `putObject(String field)` — создать вложенный ObjectNode.    
- `putArray(String field)` — создать вложенный ArrayNode.