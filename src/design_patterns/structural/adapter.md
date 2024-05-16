# Adapter

Adapter pattern is pattern part of the Structural Design Patterns. It allows objects with incompatible interfaces to collaborate.

```rust, noplayground
trait Target {
    fn request(&self) -> String;
}

struct Adaptee;

impl Adaptee {
    fn specific_request(&self) -> String {
        String::from("Adaptee: specific request")
    }
}

struct Adapter {
    adaptee: Adaptee,
}

impl Adapter {
    fn new(adaptee: Adaptee) -> Self {
        Self { adaptee }
    }
}

impl Target for Adapter {
    fn request(&self) -> String {
        self.adaptee.specific_request()
    }
}

fn client_code(target: &dyn Target) {
    println!("Client: I'm using the Target interface: {}", target.request());
}    
```
