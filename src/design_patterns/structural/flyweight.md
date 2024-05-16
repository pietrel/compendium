# Flyweight

Flyweight is a structural design pattern that allows programs to support vast quantities of objects by keeping their memory consumption low.

The Flyweight pattern is used to reduce the memory usage or computational expenses by sharing as much as possible with similar objects. It is used to minimize memory usage or computational expenses by sharing as much as possible with similar objects.

```rust
use std::collections::HashMap;

struct FlyweightFactory {
    flyweights: HashMap<String, Flyweight>,
}

impl FlyweightFactory {
    fn new() -> Self {
        Self {
            flyweights: HashMap::new(),
        }
    }

    fn get_flyweight(&mut self, key: String) -> Flyweight {
        if !self.flyweights.contains_key(&key) {
            self.flyweights.insert(key.clone(), Flyweight::new(key));
        }
        self.flyweights.get(&key).unwrap().clone()
    }
}

struct Flyweight {
    key: String,
}

impl Flyweight {
    fn new(key: String) -> Self {
        Self { key }
    }

    fn operation(&self) -> String {
        format!("Flyweight: {}", self.key)
    }
}

fn main() {
    let mut factory = FlyweightFactory::new();
    let flyweight1 = factory.get_flyweight("key1".to_string());
    let flyweight2 = factory.get_flyweight("key2".to_string());
    let flyweight3 = factory.get_flyweight("key1".to_string());

    println!("{}", flyweight1.operation());
    println!("{}", flyweight2.operation());
    println!("{}", flyweight3.operation());
}
```
