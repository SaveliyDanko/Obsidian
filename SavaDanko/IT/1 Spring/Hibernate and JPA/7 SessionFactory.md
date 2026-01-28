`SessionFactory` - Создает и управляет сессиями (объектами `Session`). Является фабрикой сессий.
- Создание сессий: Управляет объектами `Session`.
- Кэширование: Поддерживает кэш первого уровня.
- Оптимизация: Предполагается единственный экземпляр на приложение (Singleton).
- Конфигурация: Загружает параметры из файла `hibernate.cfg.xml` или из кода.
```java
SessionFactory sessionFactory = new Configuration()  
        .configure()  
        .addAnnotatedClass(Person.class)  
        .buildSessionFactory();
```



