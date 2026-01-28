---
tags:
  - review
sr-due: 2026-07-10
sr-interval: 167
sr-ease: 270
---

---
**Type Aliases** — это способ дать имя любому типу в TypeScript (объекту, union, примитиву и т. д.), чтобы переиспользовать его.
```ts
type Point = { x: number; y: number };
type ID = number | string;
```
Это только псевдонимы — они не создают новый уникальный тип, а полностью эквивалентны исходному.