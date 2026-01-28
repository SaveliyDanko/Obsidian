#rust 

---
	A **function** in Rust is a block of code that performs a task. It’s defined using the `fn` keyword and is statically typed — meaning argument and return types must always be known at compile time.

```rust
fn greet(name: &str) -> String {
    format!("Hello, {}!", name)
}
```

**Note**: The last expression (without `;`) is the return value.

---
#### 1. Type Annotations Required
```rust
fn add(x: i32, y: i32) -> i32 {
    x + y
}
```
Rust does not allow implicit return types or untyped parameters.

---
#### 2. No `return` Needed (but you can use it)
```rust
fn double(x: i32) -> i32 {
    x * 2  // implicit return
}

fn double_explicit(x: i32) -> i32 {
    return x * 2;  // explicit return
}
```

---
#### 3. No Function Overloading
Rust does not support function overloading (same name, different parameters). Use:
- traits (`impl`)
- enums
- generics
    
---
#### 4. Main Function (`fn main`)
Every executable starts from:
```rust
fn main() {
    println!("Hello, world!");
}
```

---
- Use `snake_case` for function names.