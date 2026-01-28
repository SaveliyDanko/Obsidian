---
tags:
  - review
sr-due: 2026-03-28
sr-interval: 85
sr-ease: 250
---

---
[[13 @PropertySource]]

---
[Article](https://www.baeldung.com/spring-value-annotation)

---
This `@Value` annotation can be used for injecting values into fields in Spring-managed beans, and it can be applied at the field or constructor/method parameter level.

Let’s define the properties file:
```application.properties
value.from.file=Value got from the file
priority=high
listOfValues=A,B,C
```

In the following example, we get Value got from the file assigned to the field:
```java
@Value("${value.from.file}")
private String valueFromFile;
```

Let’s assume that we have defined a system property named system Value:
```java
@Value("${systemValue}")
private String systemValue;
```

Default values can be provided for properties that might not be defined. Here, the value some default will be injected:
```java
@Value("${unknown.param:some default}")
private String someDefault;
```

Sometimes, we need to inject a bunch of values. It would be convenient to define them as comma-separated values for the single property in the properties file or as a system property and to inject into an array.

In the first section, we defined comma-separated values in the listOfValues of the properties file_,_ so the array values would be `[“A”, “B”, “C”]`:
```java
@Value("${listOfValues}")
private String[] valuesArray;
```

First, we’ll need to define the property in the `{key: ‘value’ }` form in our properties file:
```application.properties
valuesMap={key1: '1', key2: '2', key3: '3'}
```

Now we can inject this value from the property file as a Map:
```java
@Value("#{${valuesMap}}")
private Map<String, Integer> valuesMap;
```

###### **Constructor Injection**
When we use the `@Value` annotation, we’re not limited to a field injection. We can also use it together with constructor injection.
```java
@Component
@PropertySource("classpath:values.properties")
public class PriorityProvider {

    private String priority;

    @Autowired
    public PriorityProvider(@Value("${priority:normal}") String priority) {
        this.priority = priority;
    }

    // standard getter
}
```

###### **Setter Injection**
```java
@Component
@PropertySource("classpath:values.properties")
public class CollectionProvider {

    private List<String> values = new ArrayList<>();

    @Autowired
    public void setValues(@Value("#{'${listOfValues}'.split(',')}") List<String> values) {
        this.values.addAll(values);
    }

    // standard getter
}
```
