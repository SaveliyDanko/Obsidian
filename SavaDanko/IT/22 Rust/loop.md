#rust 

---
**loop**
The `loop` keyword tells Rust to execute a block of code over and over again forever or until you explicitly tell it to stop.
```rust
fn main() {
    loop {
        println!("again!");
    }
}
```
- `break`
- `continue`

**Returning Values from Loops**
You might also need to pass the result of that operation out of the loop to the rest of your code. To do this, you can add the value you want returned after the `break` expression you use to stop the loop;
```rust
fn main() {
		let mut counter = 0;

		let result = loop {
		        counter += 1;

		        if counter == 10 {
				        break counter * 2;
			    }
	    };

		println!("The result is {result}");
}
```

**break-continue label**
It is possible to make break and continue to different nested loops if you use loop naming.
```rust
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

**while loop**
```rust
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

**for loop**
```rust
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

```rust
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```