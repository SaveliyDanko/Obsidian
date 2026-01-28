---
tags:
  - review
sr-due: 2026-02-16
sr-interval: 70
sr-ease: 250
---

---
**Идея:**  
Клиенты не должны зависеть от методов, которые они не используют. Вместо «толстых» интерфейсов — набор маленьких, точных «по ролям».

###### **Плохой пример (нарушение ISP)**
```java
public interface MultiFunctionDevice {
    void print(String doc);
    void scan(String doc);
    void fax(String doc);
}

public class SimplePrinter implements MultiFunctionDevice {
    @Override public void print(String doc) { /* ok */ }
    
    @Override public void scan(String doc) {
	     throw new UnsupportedOperationException(); 
     }
    
    @Override public void fax(String doc)  { 
	    throw new UnsupportedOperationException(); 
    }
}
```
Клиенту «принтера» навязали скан и факс.

###### **Хороший пример (сегрегация интерфейсов)**
```java
public interface Printer {
    void print(String doc);
}

public interface Scanner {
    void scan(String doc);
}

public interface Fax {
    void fax(String doc);
}

// Класс, которому нужен только принт:
public class SimplePrinter implements Printer {
    @Override public void print(String doc) { /* печать */ }
}

// Комбинированное устройство через композицию:
public class OfficeMFD implements Printer, Scanner, Fax {
    @Override public void print(String doc) { /* ... */ }
    @Override public void scan(String doc)  { /* ... */ }
    @Override public void fax(String doc)   { /* ... */ }
}
```
Клиенты зависят только от нужных контрактов; реализация может комбинировать роли.
