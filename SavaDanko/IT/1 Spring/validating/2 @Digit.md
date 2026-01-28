---
tags:
  - review
sr-due: 2026-01-29
sr-interval: 1
sr-ease: 230
---

---
`@Digit`
The annotated element must be a number within accepted range.

Supported types are:
- BigDecimal
- BigInteger
- CharSequence
- byte, short, int, long, and their respective wrapper types
- null elements are considered valid.
```java
@Digits(integer = 3, fraction = 1)
private BigDecimal number;
```