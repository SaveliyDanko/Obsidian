---
tags:
  - review
sr-due: 2026-03-03
sr-interval: 38
sr-ease: 230
---

---
```java
@Component  
class MyBean implements BeanNameAware, ApplicationContextAware, InitializingBean, DisposableBean {  
  
    private String beanName;  
    private ApplicationContext context;  
    private ConstructorDependency constructorDependency;  
  
    public MyBean(ConstructorDependency constructorDependency) {  
        this.constructorDependency = constructorDependency;  
        System.out.println("1. Конструктор MyBean вызван (Instantiation)");  
        System.out.println("2. Зависимость ConstructorDependency внедрена (DI)");  
    }  
  
    @Override  
    public void setBeanName(String name) {  
        this.beanName = name;  
        System.out.println("3. BeanNameAware: Имя бина - " + name);  
    }  
  
    @Override  
    public void setApplicationContext(ApplicationContext applicationContext) throws BeansException {  
        this.context = applicationContext;  
        System.out.println("3. ApplicationContextAware: Контекст передан");  
    }  
  
    @PostConstruct  
    public void postConstruct() {  
        System.out.println("5. @PostConstruct: Бин проинициализирован");  
    }  
  
    @Override  
    public void afterPropertiesSet() {  
        System.out.println("5. InitializingBean: Бин завершил инициализацию");  
    }  
  
    @PreDestroy  
    public void preDestroy() {  
        System.out.println("7. @PreDestroy: Перед уничтожением бина");  
    }  
  
    @Override  
    public void destroy() {  
        System.out.println("7. DisposableBean: Бин уничтожен");  
    }  
}  
  
// Дополнительный бин для DI  
@Component  
class ConstructorDependency {  
    public ConstructorDependency() {  
        System.out.println("1. Конструктор ConstructorDependency вызван (Instantiation)");  
    }  
}  
  
// BeanPostProcessor для логирования этапов postProcessBeforeInitialization и postProcessAfterInitialization  
@Component  
class MyBeanPostProcessor implements BeanPostProcessor {  
  
    @Override  
    public Object postProcessBeforeInitialization(Object bean, String beanName) {  
        if (bean instanceof MyBean) {  
            System.out.println("4. BeanPostProcessor: Before Init - " + beanName);  
        }  
        return bean;  
    }  
  
    @Override  
    public Object postProcessAfterInitialization(Object bean, String beanName) {  
        if (bean instanceof MyBean) {  
            System.out.println("6. BeanPostProcessor: After Init - " + beanName);  
        }  
        return bean;  
    }  
}  
  
@SpringBootApplication  
public class DemoApplication {  
    public static void main(String[] args) {  
        SpringApplication.run(DemoApplication.class, args);  
    }  
  
}
```

`1. Конструктор ConstructorDependency вызван (Instantiation)`
`1. Конструктор MyBean вызван (Instantiation)`
`2. Зависимость ConstructorDependency внедрена (DI)`
`3. BeanNameAware: Имя бина - myBean`
`3. ApplicationContextAware: Контекст передан`
`4. BeanPostProcessor: Before Init - myBean`
`5. @PostConstruct: Бин проинициализирован`
`5. InitializingBean: Бин завершил инициализацию`
`6. BeanPostProcessor: After Init - myBean`
`7. @PreDestroy: Перед уничтожением бина`
`7. DisposableBean: Бин уничтожен`

