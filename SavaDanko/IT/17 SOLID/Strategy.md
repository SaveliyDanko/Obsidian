---
tags:
  - review
sr-due: 2026-04-09
sr-interval: 113
sr-ease: 270
---

---
**Strategy** is a behavioral pattern that lets you swap an algorithm (the strategy) at runtime without changing the code that uses it. You encapsulate related algorithms behind a common interface and delegate work to the chosen implementation.

###### **When to use**
- You have several ways to do the same task (e.g., payment methods, compression formats, pricing rules).
- Branchy code like `if/else` or `switch` is growing with “choose algorithm” logic.
- You want to unit-test algorithms independently and vary them at runtime/config time.

###### **Structure (conceptual)**
- `Strategy (interface)` — contract for the algorithm.
- `ConcreteStrategy` — specific algorithm implementations.
- `Context` — holds a Strategy and delegates to it.

###### **Java example**
```java
// Strategy
public interface PaymentStrategy {
    void pay(long cents);
}

// Concrete strategies
public class CardPayment implements PaymentStrategy {
    @Override 
    public void pay(long cents) { System.out.println("Paid by card: " + cents); }
}
public class PaypalPayment implements PaymentStrategy {
    @Override 
    public void pay(long cents) { System.out.println("Paid by PayPal: " + cents); }
}

// Context
public class Checkout {
    private PaymentStrategy strategy;
    public Checkout(PaymentStrategy strategy) { this.strategy = strategy; }
    public void setStrategy(PaymentStrategy strategy) { this.strategy = strategy; }
    public void complete(long cents) { strategy.pay(cents); }
}

// Client
Checkout co = new Checkout(new CardPayment());
co.complete(2599);                 // card
co.setStrategy(new PaypalPayment());
co.complete(2599);                 // PayPal
```

###### **Implementation tips**
- Keep the Strategy interface minimal (single method if possible).
- Make strategies stateless or immutable.
- Provide sensible defaults in the Context.
- For discoverability, collect strategies in a registry/map keyed by name/enum.
- Consider enum strategies when the set is small and closed:
```java
enum RoundingStrategy {
  UP { public long round(double v) { return (long)Math.ceil(v); } },
  DOWN { public long round(double v) { return (long)Math.floor(v); } };
  public abstract long round(double v);
}
```
