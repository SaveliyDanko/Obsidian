`@Produces` указывает какой медиа-тип (Content-Type) возвращает ресурс:
- Вешается на класс или метод (перекрывает класс).
```java
@Path("/greetings")
@Produces(MediaType.APPLICATION_JSON)
public class GreetingResource {
  @GET
  public Greeting get() { ... }

  @GET @Path("text")
  @Produces(MediaType.TEXT_PLAIN)
  public String asText() { return "hi"; }
}
```
