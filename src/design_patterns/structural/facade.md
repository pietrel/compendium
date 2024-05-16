# Facade

The Facade pattern is a structural design pattern that provides a simplified interface to a complex system of classes, library, or framework. It is used to hide the complexities of the system and provide an interface to the client using which the client can access the system.

The Facade pattern is used to provide a simple interface to a complex system. It is used to hide the complexities of the system and provide an interface to the client using which the client can access the system.

```rust
struct Subsystem1;

impl Subsystem1 {
    fn operation1(&self) -> String {
        "Subsystem1: Ready!".to_string()
    }
}

struct Subsystem2;

impl Subsystem2 {
    fn operation1(&self) -> String {
        "Subsystem2: Get ready!".to_string()
    }
}

struct Facade {
    subsystem1: Subsystem1,
    subsystem2: Subsystem2,
}

impl Facade {
    fn new(subsystem1: Subsystem1, subsystem2: Subsystem2) -> Self {
        Self {
            subsystem1,
            subsystem2,
        }
    }

    fn operation(&self) -> String {
        let mut result = "Facade initializes subsystems:\n".to_string();
        result += &self.subsystem1.operation1();
        result += &self.subsystem2.operation1();
        result
    }
}

fn main() {
    let subsystem1 = Subsystem1;
    let subsystem2 = Subsystem2;
    let facade = Facade::new(subsystem1, subsystem2);
    println!("{}", facade.operation());
}
```
