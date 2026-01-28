#rust 

---
[[IT/22 Rust/data types]]

---

| Length  | Signed  | Unsigned |
| ------- | ------- | -------- |
| 8-bit   | `i8`    | `u8`     |
| 16-bit  | `i16`   | `u16`    |
| 32-bit  | `i32`   | `u32`    |
| 64-bit  | `i64`   | `u64`    |
| 128-bit | `i128`  | `u128`   |
| arch    | `isize` | `usize`  |

---
**Типы `isize` и `usize`**
Типы `isize` и `usize` — это специальные целочисленные типы, которые зависят от архитектуры процессора:
- на 64-битной системе → `isize` и `usize` имеют 64 бита
- на 32-битной системе → 32 бита

---

| Number literals  | Example       |
| ---------------- | ------------- |
| Decimal          | `98_222`      |
| Hex              | `0xff`        |
| Octal            | `0o77`        |
| Binary           | `0b1111_0000` |
| Byte (`u8` only) | `b'A'`        |
