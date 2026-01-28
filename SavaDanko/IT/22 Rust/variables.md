#rust 

---
```rust
let x = 5;            // immutable variable by defauld
let mut x = 5;     // mutable variable
```

Constant declaration:
```rust
const THREE_HOURS_IN_SECONDS: u32 = 60 * 60 * 3;
```

Shadowing:
```rust
fn main() {
    let x = 5;
    let x = x + 1;
    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}");
    }
    println!("The value of x is: {x}");
}
```
