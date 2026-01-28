---
tags:
  - review
sr-due: 2026-01-29
sr-interval: 1
sr-ease: 230
---

---
`@Min`
The annotated element must be a number whose value must be higher or equal to the specified minimum.
- `value` $-$ value the element must be higher or equal to

`@Max`
The annotated element must be a number whose value must be lower or equal to the specified maximum.
- `value` $-$ value the element must be lower or equal to

The annotated element must be a number whose value must be lower or equal to the specified maximum.

Supported types are:
- BigDecimal
- BigInteger
- byte, short, int, long, and their respective wrappers
- Note that double and float are not supported due to rounding errors (some providers might provide some approximative support).
- null elements are considered valid.