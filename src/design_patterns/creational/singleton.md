# Singleton

The Singleton pattern is a creational design pattern that ensures a class has only one instance and provides a global point of access to it. It is useful when you need to restrict the instantiation of a class to a single object and provide a single point of access to a resource.

### Implementation in Rust

A pure safe way to implement Singleton in Rust is using no global variables at all and passing everything around through function arguments. The oldest living variable is an object created at the start of the `main()`

```rust
fn change(global_state: &mut u32) {
    *global_state += 1;
}

fn main() {
    let mut global_state = 0u32;

    change(&mut global_state);
    println!("Final state: {}", global_state);

    change(&mut global_state);
    println!("Final state: {}", global_state);
}
```

#### Using `mutex`

Starting with `Rust 1.63`, it can be easier to work with global mutable singletons, although it's still preferable to avoid global variables in most cases.

Now that `Mutex::new` is const, you can use global static `Mutex` locks without needing lazy initialization.

```rust
use std::sync::Mutex;

static ARRAY: Mutex<Vec<i32>> = Mutex::new(Vec::new());

fn do_a_call() {
    ARRAY.lock().unwrap().push(1);
}

fn main() {
    do_a_call();
    do_a_call();
    do_a_call();

    println!("Called {} times", ARRAY.lock().unwrap().len());
}
```
