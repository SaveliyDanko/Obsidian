---
tags:
  - review
sr-due: 2026-03-23
sr-interval: 78
sr-ease: 250
---

---
	**Rest (остаток)** — при  деструктуризации
```ts
const [first, ...rest] = [1, 2, 3, 4];

console.log(first); // 1
console.log(rest);  // [2, 3, 4]
```

**Spread (распаковка)** — при создании массива или объекта
```ts
const nums1 = [1, 2];
const nums2 = [3, 4];

const all = [...nums1, ...nums2]; // [1, 2, 3, 4]
```