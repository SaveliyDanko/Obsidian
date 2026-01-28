`@Path` (пакет `jakarta.ws.rs`) задаёт URI-путь для:
- ресурс-класса — базовый сегмент
- ресурс-метода — добавочный сегмент.
    
Полный путь = `@ApplicationPath` + `@Path` у класса + `@Path` у метода
```java
@ApplicationPath("api")
public class RestConfig extends Application {}

@Path("/greetings")               // класс: /api/greetings
public class GreetingResource {

  @GET
  @Path("/{id}")                  // метод: /api/greetings/{id}
  public Greeting get(@PathParam("id") long id) { ... }
}
```

#### Шаблоны пути и параметры
Внутри `@Path` можно использовать шаблоны в фигурных скобках:
- `@Path("/{id}")` → `@PathParam("id") long id`
- По умолчанию параметр совпадает с одним сегментом (`[^/]+`), т.е. не захватывает `/`.
    
- Можно ограничить значение регуляркой:  
    `@Path("/{id:\\d+}")` — только цифры.
```java
@GET @Path("/{name:[A-Za-z]+}")      // только буквы
public Response byName(@PathParam("name") String n) { ... }
```
