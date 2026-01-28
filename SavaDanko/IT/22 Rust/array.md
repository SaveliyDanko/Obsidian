#rust 

---
[[IT/22 Rust/data types]]

---
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];
}
```
- Must have the same type
- Have a fixed length

You write an array’s type using square brackets with the type of each element, a semicolon, and then the number of elements in the array, like so:
```rust
let a: [i32; 5] = [1, 2, 3, 4, 5];
```

You can also initialize an array to contain the same value for each element by specifying the initial value, followed by a semicolon, and then the length of the array in square brackets, as shown here:
```rust
let a = [3; 5];
```

You can access elements of an array using indexing:
```rust
fn main() {
    let a = [1, 2, 3, 4, 5];

    let first = a[0];
    let second = a[1];
}
```
