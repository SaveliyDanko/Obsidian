#rust 

---
- Each value in Rust has an _owner_.
- There can only be one owner at a time.
- When the owner goes out of scope, the value will be dropped.

```rust
{
		let s = String::from("hello"); // s is valid from this point forward

		// do stuff with s
}      // this scope is now over, and s is 
		// longer valid
```

There is a natural point at which we can return the memory our `String` needs to the allocator: when `s` goes out of scope. When a variable goes out of scope, Rust calls a special function for us. This function is called [`drop`](https://doc.rust-lang.org/std/ops/trait.Drop.html#tymethod.drop), and it’s where the author of `String` can put the code to return the memory. Rust calls `drop` automatically at the closing curly bracket.