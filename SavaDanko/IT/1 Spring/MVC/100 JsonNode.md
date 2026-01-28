**### **JsonNode в Java: Подробное руководство**

---

#### **1. Тезис:**

`JsonNode` — это класс из библиотеки **Jackson**, предназначенный для представления узлов в JSON-дереве. Он позволяет парсить, модифицировать и работать с JSON-структурами в виде дерева.

|Класс|Описание|
|---|---|
|`ObjectMapper`|Класс для преобразования JSON в объекты и обратно.|
|`JsonNode`|Базовый класс для представления узла JSON.|
|`ObjectNode`|Представляет JSON-объект (ключ-значение).|
|`ArrayNode`|Представляет JSON-массив.|
|`JsonParser`|Используется для построчного парсинга больших файлов.|

---

### **5. Пример использования JsonNode:**

#### **5.1 Преобразование JSON-строки в JsonNode:**

```java
import com.fasterxml.jackson.databind.JsonNode;
import com.fasterxml.jackson.databind.ObjectMapper;

public class JsonNodeExample {
    public static void main(String[] args) throws Exception {
        String json = "{\"name\":\"Saveliy\", \"age\":30}";

        ObjectMapper mapper = new ObjectMapper();
        JsonNode node = mapper.readTree(json);

        System.out.println("Name: " + node.get("name").asText());
        System.out.println("Age: " + node.get("age").asInt());
    }
}
```

##### **Результат:**

```
Name: Saveliy  
Age: 30  
```

---

### **6. Чтение JSON из файла:**

```java
JsonNode rootNode = mapper.readTree(new File("user.json"));
String name = rootNode.get("name").asText();
int age = rootNode.get("age").asInt();
System.out.println("Name: " + name + ", Age: " + age);
```

##### **user.json:**

```json
{
  "name": "Alex",
  "age": 25
}
```

##### **Результат:**

```
Name: Alex, Age: 25  
```

---

### **7. Основные методы JsonNode:**

|Метод|Описание|
|---|---|
|`get(String fieldName)`|Получает значение по имени поля.|
|`get(int index)`|Получает значение по индексу (для массивов).|
|`asText()`|Преобразует узел в строку.|
|`asInt()`|Преобразует узел в целое число.|
|`asBoolean()`|Преобразует узел в логическое значение.|
|`size()`|Возвращает количество элементов (для массивов).|
|`isObject()`|Проверяет, является ли узел объектом.|
|`isArray()`|Проверяет, является ли узел массивом.|
|`isMissingNode()`|Проверяет, отсутствует ли узел.|
|`path(String fieldName)`|Безопасное получение узла (не выбрасывает исключение).|

---

### **8. Работа с вложенными объектами:**

```java
String json = """
{
  "user": {
    "name": "Saveliy",
    "address": {
      "city": "Tbilisi",
      "country": "Georgia"
    }
  }
}""";

JsonNode root = mapper.readTree(json);
JsonNode address = root.path("user").path("address");

String city = address.get("city").asText();
String country = address.get("country").asText();

System.out.println("City: " + city);
System.out.println("Country: " + country);
```

##### **Результат:**

```
City: Tbilisi  
Country: Georgia  
```

###### ==Объединение узлов:==
```java
ObjectNode address = mapper.createObjectNode();
address.put("city", "Tbilisi");
address.put("country", "Georgia");

ObjectNode user = mapper.createObjectNode();
user.put("name", "Saveliy");
user.put("age", 30);
user.set("address", address);

System.out.println(mapper.writerWithDefaultPrettyPrinter().writeValueAsString(user));
```

###### **Результат:**
```json
{
  "name": "Saveliy",
  "age": 30,
  "address": {
    "city": "Tbilisi",
    "country": "Georgia"
  }
}
```
