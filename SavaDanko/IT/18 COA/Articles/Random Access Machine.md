#coa

---
Writing algorithms is a complex task, to deal with this problem various models called abstract machines were designed hypothetically.

**There are two types of Abstract Machine**
- Random Access Machine (RAM)  
- Parallel Random Access Machine (PRAM)

**Random Access Machine (RAM)**
![[Pasted image 20250604160119.png]]
It is a potentially unbound bank of memory cells, each of which can contain an arbitrary number or character.
Memory cells are numbered and it takes time to access any cell in memory or say all operations (read/write from memory, standard arithmetic, and Boolean operations) take a unit of time.
- The Random Access Machine (RAM) model is a one address computer.
- RAM is a sequential machine.
- RAM consists of memory, read-only input tape, output tape only, and writes a program.
- RAM consists of memory, read-only input tape and output tape only.
- The program is not stored in memory and cannot be modified.
- The input tape consists of a series of integers. Each time an input value is read, the input head moves forward one square.
- Similarly, the output head moves forward after each write.
- Memory consists of an infinite sequence of registers, designated `r0`, `r1`, `r2`,…. Each register can contain an integer.
- Register `r0` is the accumulator, where the calculation is done.
- RAM must have the same instructions as `LOAD`, `STORE`, `READ`, `WRITE`, `ADD`, `SUBTRACT`, `MULTIPLY`, `DIVIDE`, `TEST`, `JUMP`, and `HALT`.
- We assume that each of these steps takes a constant, that is, `O(1)` time.

