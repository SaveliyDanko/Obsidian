---
tags:
  - review
sr-due: 2026-01-31
sr-interval: 29
sr-ease: 250
---

---
Файл конфигурации hibernate
```xml
<hibernate-configuration>  
    <session-factory>  
        <!-- Драйвер JDBC -->  
        <property name="hibernate.connection.driver_class">org.postgresql.Driver</property>  
  
        <!-- URL базы данных -->  
        <property name="hibernate.connection.url">jdbc:postgresql://localhost:5432/savadankoDB</property>  
  
        <!-- Логин и пароль -->  
        <property name="hibernate.connection.username">postgres</property>  
        <property name="hibernate.connection.password">postgres</property>  
  
        <!-- Диалект базы данных -->  
        <property name="hibernate.dialect">org.hibernate.dialect.PostgreSQLDialect</property>  
  
        <!-- Автоматическое создание таблиц -->  
        <property name="hibernate.hbm2ddl.auto">update</property>  
  
        <!-- Логирование SQL-запросов -->  
        <property name="hibernate.show_sql">true</property>  
        <property name="hibernate.format_sql">true</property>  
  
        <property name="hibernate.current_session_context_class">thread</property>  
    </session-factory>  
	</hibernate-configuration>
```