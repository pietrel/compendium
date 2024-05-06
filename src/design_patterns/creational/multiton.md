# Multiton

The multiton pattern is a variation of the singleton pattern, designed to support multiple instances of a single class, each identified by a unique key. This approach is advantageous in scenarios where a singleton's single-instance limitation is too restrictive, but where the total number of instances is finite and predetermined.

Like the singleton, the multiton employs a private constructor and a static method to manage its instances. The key difference lies in the static method, which accepts a unique identifier as an argument. This identifier determines whether a corresponding instance already exists: if it does, that instance is returned; if not, a new instance is created, stored, and then returned.

The multiton pattern ensures that a class can have multiple instances, each distinguished by a unique identifier, thus managing instance creation in a controlled manner. This is particularly useful when you need several instances of a class but want to limit their number to prevent excessive resource use.

To implement the multiton pattern, define a class with a private constructor to block direct instantiation. Then, provide a static method that takes a unique identifier for the desired instance. When this method is called, it either retrieves an existing instance linked to that identifier or creates and stores a new one, ensuring that each identifier is associated with a single instance.

This setup allows controlled access and distinct management of multiple instances based on their unique identifiers, ensuring that each is created only once.

### Example Implementation in Rust

```rust
use std::collections::HashMap;
use std::sync::{Arc, Mutex};

#[derive(Debug, Clone)]
struct MyType {
    id: String,
    data: String,
}

struct Multiton {
    instances: Mutex<HashMap<String, Arc<MyType>>>,
}

impl Multiton {
    // Initializes a new Multiton manager
    fn new() -> Multiton {
        Multiton {
            instances: Mutex::new(HashMap::new()),
        }
    }

    // Retrieves an existing instance or creates a new one if it does not exist
    fn get_instance(&self, id: &str) -> Arc<MyType> {
        let mut instances = self.instances.lock().unwrap();
        instances.entry(id.to_string()).or_insert_with(|| {
            Arc::new(MyType {
                id: id.to_string(),
                data: format!("Data for {}", id),
            })
        }).clone()
    }
}
fn main() {
    let multiton = Multiton::new();

    // Retrieve an instance with ID "instance1"
    let instance1 = multiton.get_instance("instance1");
    println!("Retrieved: {:?}", instance1);

    // Retrieve the same instance again to demonstrate that it returns the same object
    let same_instance1 = multiton.get_instance("instance1");
    println!("Retrieved again: {:?}", same_instance1);

    // Retrieve a different instance with ID "instance2"
    let instance2 = multiton.get_instance("instance2");
    println!("Retrieved: {:?}", instance2);
}



```
