---
tags:
  - review
sr-due: 2026-07-12
sr-interval: 169
sr-ease: 270
---

---
###### **Идея**
* Высокоуровневые модули не должны зависеть от низкоуровневых. Оба зависят от абстракций.
* Абстракции не должны зависеть от деталей. Детали (реализации) должны зависеть от абстракций.

###### **Анти-пример (нарушение DIP)**
```java
class OrderService {
    private final StripeClient stripe = new StripeClient("api-key"); // Жёсткая зависимость

    public void pay(Order order) {
        stripe.charge(order.getAmount()); // Нельзя подменить, трудно тестировать
    }
}
```
* `OrderService` зависит от конкретного `StripeClient`. Чтобы добавить PayPal — придётся менять `OrderService`.

###### **Правильный подход (инвертируем зависимости)**
```java
// 1) Абстракция — стабильный контракт
public interface PaymentProcessor {
    void charge(long amountCents);
}

// 2) Реализации — детали
public class StripeProcessor implements PaymentProcessor {
    private final String apiKey;
    public StripeProcessor(String apiKey) { this.apiKey = apiKey; }
    @Override public void charge(long amountCents) { /* вызов Stripe */ }
}

public class PaypalProcessor implements PaymentProcessor {
    private final String clientId;
    public PaypalProcessor(String clientId) { this.clientId = clientId; }
    @Override public void charge(long amountCents) { /* вызов PayPal */ }
}

// 3) Высокоуровневый модуль зависит от абстракции
public class OrderService {
    private final PaymentProcessor payment;
    public OrderService(PaymentProcessor payment) { // конструкторная инъекция
        this.payment = payment;
    }
    public void pay(Order order) {
        payment.charge(order.getAmount());
    }
}
```
