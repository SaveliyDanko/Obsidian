---
tags:
  - review
sr-due: 2026-01-29
sr-interval: 1
sr-ease: 230
---
---
The string has to be a well-formed email address. Exact semantics of what makes up a valid email address are left to Jakarta Validation providers. Accepts CharSequence.
null elements are considered valid.
- `regexp` $-$ an additional regular expression the annotated element must match. The default is any string `.*`
```java
public class UserRegistration {

    @Email(message = "Please, input correct e-mail")
    @NotBlank
    private String email;
}
```
