---
tags:
  - review
sr-due: 2026-01-28
sr-interval: 3
sr-ease: 250
---

---
`ResponseEntity` — класс, который представляет собой полный HTTP-ответ, позволяя разработчику программно управлять его статус-кодом, заголовками и телом.
```java
@GetMapping("/books/{id}")
public ResponseEntity<Book> getBook(@PathVariable Long id) {
    Book book = bookService.findById(id);

    if (book != null) {
        // Возвращаем 200 OK и саму книгу в теле
        return ResponseEntity.ok(book); 
    } else {
        // Возвращаем 404 Not Found без тела
        return ResponseEntity.notFound().build(); 
    }
}
```