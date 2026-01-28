---
tags:
  - review
sr-due: 2026-01-31
sr-interval: 21
sr-ease: 210
---

---
[Decorator](https://refactoring.guru/ru/design-patterns/decorator)

---
Паттерн Декоратор динамически наделяет объект новыми возможностями и является гибкой альтернативой субклассированию в области расширения функциональности.
Классический пример в JDK — цепочки `InputStream` / `Reader` (например, `BufferedInputStream(new GZIPInputStream(...))`).

###### **Пример на Java**
Сценарий: у нас есть уведомления. Базово — e-mail. Декораторами добавим SMS, Slack и шифрование перед отправкой.
```java
import java.util.*;

// 1. Интерфейс
interface Notifier {
    void send(String msg);
}

// 2. Базовый компонент
record EmailNotifier(String email) implements Notifier {
    public void send(String msg) {
        System.out.println("Email to " + email + ": " + msg);
    }
}

// 3. Базовый декоратор (можно сделать лаконичным)
abstract class Decorator implements Notifier {
    protected final Notifier wrapper;
    
    Decorator(Notifier n) {
	    this.wrapper = n; 
	}
    
    public void send(String msg) { 
	    wrapper.send(msg); 
	}
}

// 4. Конкретные декораторы (в одну строку)
class SmsDecorator extends Decorator {
    SmsDecorator(Notifier n) {
	    super(n); 
	}
    
    public void send(String msg) {
	    super.send(msg); 
	    System.out.println("SMS: " + msg); 
	}
}

class EncryptDecorator extends Decorator {
    EncryptDecorator(Notifier n) { 
	    super(n); 
	}
    
    public void send(String msg) { 
	    super.send("[Base64:" + Base64.getEncoder().encodeToString(msg.getBytes()) + "]"); 
	}
}

// 5. Использование
public class Main {
    public static void main(String[] args) {
        // Собираем "матрёшку" в одну строку
        Notifier n = new EncryptDecorator(
	        new SmsDecorator(
		        new EmailNotifier("boss@work.com")
		    )
        );
        n.send("Hello!");
    }
}
```