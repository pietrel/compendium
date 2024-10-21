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

### Implementation in Go

#### Using sync.Once

Go's sync.Once package offers a thread-safe method to initialize a value precisely once. This feature is perfect for implementing the Singleton pattern, eliminating the need for explicit locking mechanisms.


```go
package singleton

import "sync"

type singleton struct{}

var instance *singleton
var once sync.Once

func GetInstance() *singleton {
    once.Do(func() {
        instance = &singleton{}
    })
    return instance
}
```

#### Using `mutex`

The sync.Mutex provides a locking mechanism to ensure that only one goroutine can access the critical section of code at a time, which is useful for creating and managing the singleton instance safely.

```go
package singleton

import (
    "fmt"
    "sync"
)

type singleton struct {}

var instance *singleton
var lock = &sync.Mutex{}

func getInstance() *singleton {
    if instance == nil {
        // Only one goroutine at a time can go next
        lock.Lock()
        defer lock.Unlock()

        if instance == nil {
            fmt.Println("Instance created")
            instance = &singleton{}
        } else {
            fmt.Println("Instance exists")
        }
    } else {
        fmt.Println("Instance exists")
    }
    return instance
}
```