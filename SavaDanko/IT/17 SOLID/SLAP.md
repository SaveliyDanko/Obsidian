---
tags:
  - review
sr-due: 2026-02-28
sr-interval: 81
sr-ease: 270
---

---
SLAP — **Single Level of Abstraction Principle**

Каждая функция или метод должны работать на одном уровне абстракции. Иными словами:
- Не смешивай "что" и "как".
- Внутри функции не должно быть одновременно высокоуровневой логики и низкоуровневых деталей реализации.

###### **Пример без SLAP**
```js
function processOrder(order) {
    // Высокоуровневая идея
    console.log("Processing order...");

    // Детали низкого уровня
    const connection = createConnection("database");
    connection.open();
    const result = connection.query("SELECT * FROM products");
    connection.close();
```

###### **Пример с соблюдением SLAP**
```js
function processOrder(order) {
    console.log("Processing order...");

    const product = getProductById(order.productId);
}

function getProductById(id) {
    const connection = createConnection("database");
    connection.open();
    const product = connection.query("SELECT * FROM products");
    connection.close();
    return product;
}
```
